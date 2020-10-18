<template>
  <v-container>
    <v-row class="text-center">

      <v-col class="mb-4 mt-10">
        <h1 color="#0d253f" class="display-2 font-weight-bold mb-3">Movie Fan</h1>

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
            <Movies :isFormReady="checkFavouriteMoviesLength"/>
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
import Movies from './Movies'

export default {
  name: "Home",
  data: () => ({
    firstname: "",
    lastname: "",
    shortbio: "",
    formReady: false
  }),
  components: {
    Movies
  },
  methods: {
    checkFavouriteMoviesLength(state) {
      console.log(state)
      this.formReady = state;
    },
    debounceFirstname: debounce(function (input) {
      this.firstname = input;
    }, 450),
    debounceLastname: debounce(function (input) {
      this.lastname = input;
    }, 450),
    debounceShortbio: debounce(function (input) {
      this.shortbio = input;
    }, 450),
  },
};
</script>
