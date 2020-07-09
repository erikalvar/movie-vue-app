<template>
  <div class="movies-index">
    <h1>{{ message }}</h1>
    <div v-for="movie in movies">
      <h3>{{ movie.title }}</h3>
      <router-link v-bind:to="`/movies/${movie.id}`">Show Info</router-link>
    </div>

  </div>
</template>

<style>
</style>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      message: "Movies Index",
      movies: []
    };
  },
  created: function() {
    this.indexMovies();
  },
  methods: {
    indexMovies: function() {
      axios.get("/api/movies").then(response => {
        console.log("All Movies:", response.data);
        this.movies = response.data;
      });
    }
  }
};
</script>