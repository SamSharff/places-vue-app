<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome to a list of places!",
      places: [],
      newPlaceParams: {},
    };
  },
  created: function () {
    this.indexPlaces();
  },
  methods: {
    indexPlaces: function () {
      axios.get("/places").then((response) => {
        console.log("All places", response);
        this.places = response.data;
      });
    },
    createPlace: function () {
      axios
        .post("/places", this.newPlaceParams)
        .then((response) => {
          console.log("creating place", response);
          this.newPlaceParams = {};
        })
        .catch((error) => {
          console.log("error creating place", error.response);
        });
    },
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <!-- createPlace -->
    <div>
      Name:
      <input type="text" v-model="newPlaceParams.name" />
      Address:
      <input type="text" v-model="newPlaceParams.address" />
      <br />
      <button v-on:click="createPlace()">Add new place!</button>
    </div>
    <!-- indexPlace -->
    <div v-for="place in places" v-bind:key="place.id">
      <h2>Name: {{ place.name }}</h2>
      <h4>Address: {{ place.address }}</h4>
    </div>
  </div>
</template>

<style></style>
