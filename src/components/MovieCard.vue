<template v-model="item" v-slot:item="{ item }">
  <div>
      <v-list-item-avatar>
        <v-img :src="item.poster"></v-img>
      </v-list-item-avatar>
      <v-list-item-content>
        <v-list-item-title v-text="item.title"></v-list-item-title>
        <v-list-item-subtitle v-text="item.overview"></v-list-item-subtitle>
      </v-list-item-content>
      <v-list-item-action v-text="item.release_date"> </v-list-item-action>
    </div>
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
export default {
  name: "MovieCard",
  props: {
    item: Object
  }
}
</script>
