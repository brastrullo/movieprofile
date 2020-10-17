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

      <!-- <v-col class="ms-auto" cols="12">
        <v-text-field
          clearable
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
          clearable
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
      </v-col> -->

      <!-- <v-col class="ms-auto" cols="12" v-if="shortbio.length > 0"> -->
      <v-col class="ms-auto" cols="12">
        <v-row justify="center">
          <v-col cols="12" sm="6" md="3">
            <v-autocomplete
              chips
              deletable-chips
              multiple
              prepend-icon="mdi-video-plus-outline"
              label="Add Favourite Movies"
              placeholder="Search movies"
              :search-input.sync="query"
              v-model="moviesSelected"
              validate-on-blur
              :items="moviesFound"
              :loading="loading"
              clearable
            >
              <template v-slot:item="{ item }">
                <v-list-item>
                  <v-list-item-title>
                    {{item.title}}
                  </v-list-item-title>
                  </v-list-item>
              </template>
            </v-autocomplete>
          </v-col>
        </v-row>
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
  }),
  watch: {
    query: debounce(function (val) {
      // console.log(val)
      if (val && val.length > 0) {
        this.fetchMovies(val);
      }
    }, 450),
  },
  methods: {
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
      console.log(query);
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
