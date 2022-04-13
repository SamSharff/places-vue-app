<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome to a list of places!",
      places: [],
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
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div v-for="place in places" v-bind:key="place.id">
      <h2>Name: {{ place.name }}</h2>
      <h4>Address: {{ place.address }}</h4>
    </div>
  </div>
</template>

<style></style>
