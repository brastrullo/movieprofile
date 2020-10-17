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
          label="First Name"
          placeholder="John"
          name="firstname"
          :value="firstname"
          :updateValue="updateFirstName"
        ></v-text-field>
      </v-col>
      <v-col class="ms-auto" cols="12">
        <v-text-field
          clearable
          v-model="lastname"
          label="Last Name"
          placeholder="Doe"
          name="lastname"
          :value="lastname"
          :updateValue="updateLastName"
        ></v-text-field>
      </v-col>

      <v-col class="ms-auto" cols="12">
        <v-textarea
          counter
          clearable
          label="Short Bio"
          placeholder="Type bio..."
          name="shortbio"
          :value="shortbio"
          :updateValue="updateShortBio"
        ></v-textarea>
      </v-col>

      <v-col class="ms-auto" cols="12">
        <h2>Favourite Movies</h2>
        <v-row justify="center">
          <v-col cols="12" sm="6" md="3">
            <v-text-field prepend-icon="" label="Search movies" solo clearable></v-text-field>
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
    firstnameInput: this.$refs.firstname,
    lastnameInput: this.$refs.lastname,
    shortbioInput: this.$refs.shortbio,
  }),
};
</script>
