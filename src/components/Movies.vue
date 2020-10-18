<template>
  <v-autocomplete
    chips
    deletable-chips
    counter="15"
    multiple
    prepend-icon="mdi-video-plus-outline"
    label="Add Favourite Movies"
    placeholder="Search movies"
    @update:search-input="updateQuery"
    hide-selected
    cache-items
    return-object
    validate-on-blur
    color="blue-grey lighten-2"
    :menu-props="{ closeOnContentClick: true }"
    no-data-text="No movies found."
    item-text="title"
    item-value="id"
    v-model="moviesSelected"
    @input="moviesSelected.length >= 3 ? isFormReady(true) : isFormReady(false)"
    :items="moviesFound"
    :loading="loading"
  >
    <template v-slot:no-data>
      <v-list-item>
        <v-list-item-title> Movie not found </v-list-item-title>
      </v-list-item>
    </template>
    <template v-slot:selection="{ attr, on, item, selected }">
      <v-chip
        v-bind="attr"
        :input-value="selected"
        v-on="on"
        large
        light
        outlined
        label
        @click:close="removeMovie(item)"
        class="ma-2"
        close
      >
        <span v-text="item.title"></span>
      </v-chip>
    </template>
    <template v-slot:item="{ item }">
      <v-list-item-avatar>
        <v-img :src="item.poster"></v-img>
      </v-list-item-avatar>
      <v-list-item-content>
        <v-list-item-title v-text="item.title"></v-list-item-title>
      </v-list-item-content>
      <v-list-item-action v-text="item.release_date"> </v-list-item-action>
    </template>
  </v-autocomplete>
</template>

<script>
import debounce from "lodash.debounce";
export default {
  name: "Movies",
  data() {
    return {
      query: "",
      moviesFound: [],
      moviesSelected: [],
      loading: false,
      formReady: false
    };
  },
  props: {
    isFormReady: Function
  },
  methods: {
    updateQuery: debounce(function (val) {
      if (val && val.length > 0) {
        console.log(val);
        this.fetchMovies(val);
      }
    }, 450),
    removeMovie(movie) {
      this.moviesSelected = this.moviesSelected.filter(
          (obj) => obj.id !== movie.id
        );
    },
    fetchMovies: async function (query) {
      this.loading = true;
      const API_KEY = `ea9385095138c0c18e3aca7590507b54`;
      const BASE_URL = `https://api.themoviedb.org/3/search/movie`;
      const FETCH_URL = `${BASE_URL}?api_key=${API_KEY}&query=${encodeURIComponent(
        query
      )}&page=1`;
      const IMG_URL = `https://image.tmdb.org/t/p/w92`;

      let res = await fetch(FETCH_URL);
      let data = await res.json();
      let movies = data.results.map((obj) => ({
        id: obj.id,
        title: obj.title,
        overview: obj.overview,
        release_date: obj.release_date,
        user_score: obj.vote_average,
        poster: `${IMG_URL}${obj.poster_path}`,
      }));
      if (movies.length === 0) {
        this.errorMsg = "Movie not found";
      } else {
        this.moviesFound = movies;
        console.log({ movies });
      }
      this.loading = false;
    },
  },
};
</script>
