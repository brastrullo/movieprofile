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
      </v-col>

      <v-col class="ms-auto" cols="12" v-if="shortbio.length > 0">
        <v-row justify="center">
          <v-col cols="12" sm="6" md="3">
            <v-autocomplete
              chips
              deletable-chips
              multiple
              prepend-icon="mdi-video-plus-outline"
              label="Add Favourite Movies"
              placeholder="Search movies"
              clearable
            />
          </v-col>
        </v-row>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import debounce from 'lodash.debounce';
// import throttle from 'lodash.throttle';

export default {
  name: "Home",
  data: () => ({
    firstname: "",
    lastname: "",
    shortbio: "",
  }),
  computed: {
  },
  methods: {
    debounceFirstname: debounce(function(input) {
      this.firstname = input;
    }, 450),
    debounceLastname: debounce(function(input) {
      this.lastname = input;
    }, 450),
    debounceShortbio: debounce(function(input) {
      this.shortbio = input;
    }, 450)
  },
};
</script>
