<template>
  <div class="movies-index">
    
    <h1>{{ message }}</h1>
    Search by name: <input v-model="titleFilter" list="titles">
    <datalist id="titles">
      <option v-for="movie in movies">{{ movie.title }}</option>
    </datalist>
    <div>
      <button>Sort Alphabetically</button>
    </div>
    <div v-for="movie in orderBy(filterBy(movies, titleFilter, 'title'), 'title')">
      <h3>{{ movie.title }}</h3>
      <router-link v-bind:to="`/movies/${movie.id}`">Show Info</router-link>
    </div>

  </div>
</template>

<style>
</style>

<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";
export default {
  mixins: [Vue2Filters.mixin],
  data: function() {
    return {
      message: "Movies Index",
      movies: [],
      titleFilter: ""
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