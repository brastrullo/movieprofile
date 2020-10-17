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
          v-model="firstname"
          prepend-icon="mdi-account-edit"
          label="First Name"
          placeholder="John"
          name="firstname"
        ></v-text-field>
      </v-col>

      <v-col class="ms-auto" cols="12">
        <v-text-field
          clearable
          v-model="lastname"
          prepend-icon="mdi-account-edit-outline"
          label="Last Name"
          placeholder="Doe"
          name="lastname"
        ></v-text-field>
      </v-col>

      <v-col class="ms-auto" cols="12">
        <v-textarea
          counter
          v-model="shortbio"
          prepend-icon="mdi-card-account-details-outline"
          label="Short Bio"
          placeholder="Type bio..."
          name="shortbio"
        ></v-textarea>
      </v-col>

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
              clearable
            ></v-autocomplete>
          </v-col>
        </v-row>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "Home",
  data: () => ({
    firstname: "",
    lastname: "",
    shortbio: "",
  }),
  methods: {

  },
};
</script>
