<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12">
        <v-img
          :src="require('../assets/logo.svg')"
          class="my-3"
          contain
          height="200"
        />
      </v-col>

      <v-col class="mb-4 mt-10">
        <h1 class="display-2 font-weight-bold mb-3">Movies Fan</h1>

        <p class="subheading font-weight-regular">Please complete profile</p>
      </v-col>

      <v-col class="ms-auto" cols="12">
        <v-text-field
          prepend-icon="mdi-account-edit"
          label="First Name"
          placeholder="John"
          autocomplete="off"
          name="firstname"
          @input="debounceFirstname"
        />
      </v-col>

      <v-col class="ms-auto" cols="12" v-if="firstname.length > 0">
        <v-text-field
          prepend-icon="mdi-account-edit-outline"
          label="Last Name"
          placeholder="Doe"
          name="lastname"
          @input="debounceLastname"
        />
      </v-col>

      <v-col class="ms-auto" cols="12" v-if="lastname.length > 0">
        <v-textarea
          counter
          prepend-icon="mdi-card-account-details-outline"
          label="Short Bio"
          placeholder="Type bio..."
          name="shortbio"
          @input="debounceShortbio"
        />
      </v-col>

      <v-col class="ms-auto" cols="12" v-if="shortbio.length > 0">
        <v-row justify="center">
          <v-col cols="12">
            <v-autocomplete
              chips
              deletable-chips
              counter=15
              multiple
              prepend-icon="mdi-video-plus-outline"
              label="Add Favourite Movies"
              placeholder="Search movies"
              @update:search-input="updateQuery"
              hide-selected
              cache-items
              validate-on-blur
              color="blue-grey lighten-2"
              :menu-props="{ closeOnContentClick: true }"
              no-data-text="No movies found."
              item-text="title"
              item-value="id"
              v-model="moviesSelected"
              @input="checkFavouriteMoviesLength"
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
                <v-list-item-action v-text="item.release_date">
                </v-list-item-action>
              </template>
            </v-autocomplete>
          </v-col>
        </v-row>
      </v-col>
      <v-col v-if="formReady">
        <v-btn>Ready</v-btn>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import debounce from "lodash.debounce";
// import throttle from 'lodash.throttle';

export default {
  name: "Home",
  data: () => ({
    firstname: "",
    lastname: "",
    shortbio: "",
    loading: false,
    query: "",
    errorMsg: "",
    moviesFound: [],
    moviesSelected: [],
    formReady: false
  }),
  methods: {
    checkFavouriteMoviesLength() {
      if(this.moviesSelected.length >= 3) {
        this.formReady = true
      }
    },
    updateQuery: debounce(function (val) {
      if (val && val.length > 0) {
        console.log(val);
        this.fetchMovies(val);
      }
    }, 450),
    debounceFirstname: debounce(function (input) {
      this.firstname = input;
    }, 450),
    debounceLastname: debounce(function (input) {
      this.lastname = input;
    }, 450),
    debounceShortbio: debounce(function (input) {
      this.shortbio = input;
    }, 450),
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
