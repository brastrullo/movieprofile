<template>
<div></div>
  <!-- <article>
    <p class="title">{{ movie.title }}</p>
    <img class="poster" :src="movie.poster" :alt="movie.title" />
    <p class="overview">{{ movie.overview }}</p>
    <p class="release_date">{{ movie.release_date }}</p>
    <p :style="movie.user_score > 8 ? { color: 'green' } : { color: 'red' }">
      {{ movie.user_score }}
    </p>
  </article> -->
</template>

<script>
// export default {
//   name: "Movies",
//   data() {
//     return {
//       query: "",
//       errorMsg: "",
//       moviesFound: [],
//       moviesSelected: [],
//     };
//   },
//   props: {
//     name: String,
//     label: String,
//   },
//   methods: {
//     toggleMovie(movie) {
//       console.log(this.moviesSelected);
//       const isSelectedMovie = this.moviesSelected.find(
//         (obj) => obj.id === movie.id
//       );
//       if (!isSelectedMovie) {
//         this.moviesSelected = [...this.moviesSelected, movie];
//       } else {
//         this.moviesSelected = this.moviesSelected.filter(
//           (obj) => obj.id !== movie.id
//         );
//       }
//       console.log("movie:", movie, movie.title);
//       this.query = "";
//       this.moviesFound = [];
//     },
//     async searchMovie() {
//       const query = this.query;
//       console.log(query);
//       const API_KEY = `ea9385095138c0c18e3aca7590507b54`;
//       const BASE_URL = `https://api.themoviedb.org/3/search/movie`;
//       const FETCH_URL = `${BASE_URL}?api_key=${API_KEY}&query=${encodeURIComponent(
//         query
//       )}&page=1`;
//       const IMG_URL = `https://image.tmdb.org/t/p/w92`;

//       let res = await fetch(FETCH_URL);
//       let data = await res.json();
//       let movies = data.results.map((obj) => ({
//         id: obj.id,
//         title: obj.title,
//         overview: obj.overview,
//         release_date: obj.release_date,
//         user_score: obj.vote_average,
//         poster: `${IMG_URL}${obj.poster_path}`,
//       }));
//       if (movies.length === 0) {
//         this.errorMsg = "Movie not found";
//       } else {
//         this.moviesFound = movies;
//       }
//     },
//   },
// };
</script>
