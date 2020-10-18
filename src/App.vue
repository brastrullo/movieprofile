<template>
  <v-app>
    <v-app-bar
      app
      color="#0d253f"
      dark
    >
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          :src="require('./assets/tmdb-short.svg')"
          transition="scale-transition"
          width="100%"
        />
      </div>

      <v-spacer></v-spacer>

    </v-app-bar>

    <v-main>
      <Home />
    </v-main>
  </v-app>
</template>

<script>
import Home from './components/Home';

export default {
  name: 'App',

  components: {
    Home,
  },

  data: () => ({
    //
  }),
};
</script>
