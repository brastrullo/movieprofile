<template>
  <h2>Favourite Movies</h2>
  <p v-if="moviesSelected.length < 3 || moviesSelected.length >= 14">
    Choose between 3 to 15 movies
  </p>
  <p v-if="moviesSelected.length === 15">Max movies selected</p>
  <span v-if="moviesSelected.length > 0"
    >counter: {{ moviesSelected.length }}</span
  >
  <ul>
    <li
      class="favourite-movie"
      v-for="movie in moviesSelected"
      :key="movie.id"
      @click="toggleMovie(movie)"
    >
      {{ movie.title }}
    </li>
  </ul>
  <label v-if="moviesSelected.length < 15" :for="name">{{ label }}</label>
  <input
    v-if="moviesSelected.length < 15"
    v-model="query"
    type="text"
    :name="name"
    :id="name"
    @keydown.enter="searchMovie"
  />
  <button v-if="moviesSelected < 15" @click="searchMovie">Search</button>
  <p v-if="moviesFound.length === 0 && errorMsg.length > 0">{{ errorMsg }}</p>
  <ul v-else>
    <li
      v-for="movie in moviesFound"
      :key="movie.id"
      @click="toggleMovie(movie)"
      :class="[
        'movie-card',
        moviesSelected.find((obj) => obj.id === movie.id) === undefined
          ? ''
          : 'selected',
      ]"
    >
      <article>
        <p class="title">{{ movie.title }}</p>
        <img class="poster" :src="movie.poster" :alt="movie.title" />
        <p class="overview">{{ movie.overview }}</p>
        <p class="release_date">{{ movie.release_date }}</p>
        <p
          :style="movie.user_score > 8 ? { color: 'green' } : { color: 'red' }"
        >
          {{ movie.user_score }}
        </p>
      </article>
    </li>
  </ul>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "Movies",
  data() {
    return {
      query: "",
      errorMsg: "",
      moviesFound: [],
      moviesSelected: [],
    };
  },
  props: {
    name: String,
    label: String,
  },
  methods: {
    toggleMovie(movie) {
      console.log(this.moviesSelected);
      const isSelectedMovie = this.moviesSelected.find(
        (obj) => obj.id === movie.id
      );
      if (!isSelectedMovie) {
        this.moviesSelected = [...this.moviesSelected, movie];
      } else {
        this.moviesSelected = this.moviesSelected.filter(
          (obj) => obj.id !== movie.id
        );
      }
      console.log("movie:", movie, movie.title);
      this.query = "";
      this.moviesFound = [];
    },
    async searchMovie() {
      const query = this.query;
      console.log(query);
      const API_KEY = `ea9385095138c0c18e3aca7590507b54`;
      const BASE_URL = `https://api.themoviedb.org/3/search/movie`;
      const FETCH_URL = `${BASE_URL}?api_key=${API_KEY}&query=${encodeURIComponent(
        query
      )}&page=1`;
      const IMG_URL = `https://image.tmdb.org/t/p/w92`;
      // poster sizes from config api
      // const poster_sizes = [
      //   "w92",
      //   "w154",
      //   "w185",
      //   "w342",
      //   "w500",
      //   "w780",
      //   "original",
      // ];
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
      }
    },
  },
});
</script>

<style lang="scss" scoped>
label {
  text-align: left;
}

input {
  background: none;
  border: none;
  border-bottom: 1px solid #333;
}
button {
  margin: 0.5em 0;
}
article,
.favourite-movie,
.favourite-movie button {
  cursor: pointer;
}

article:hover,
.favourite-movie:hover {
  background: rgb(246, 246, 246);
}
.movie-card.selected {
  background: rgb(206, 206, 206);
  &:hover {
    border: 1px solid black;
  }
}
</style>
