<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome to a list of places!",
      places: [],
      newPlaceParams: {},
      currentPlace: {},
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
    showPlace: function (place) {
      console.log(place);
      this.currentPlace = place;
      document.querySelector("#place-details").showModal();
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
    <!-- indexPlace with indexShow Modal -->
    <div v-for="place in places" v-bind:key="place.id">
      <h2>Name: {{ place.name }}</h2>
      <!-- <h4>Address: {{ place.address }}</h4> -->
      <button v-on:click="showPlace(place)">More info</button>
      <dialog id="place-details">
        <form method="dialog">
          <h1>Additional details</h1>
          <p>
            Name:
            <input type="text" v-model="currentPlace.name" />
          </p>
          <p>
            Address:
            <input type="text" v-model="currentPlace.address" />
          </p>
          <button>Close</button>
        </form>
      </dialog>
    </div>
  </div>
</template>

<style></style>
