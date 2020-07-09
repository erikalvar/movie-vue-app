<template>
  <div class="movies-show">
    <h3>{{ currentMovie.title }}</h3>
    <p>Year: {{ currentMovie.year }}</p>
    <p>Plot: {{ currentMovie.plot }}</p>
    <p>Director: {{ currentMovie.director }}</p>
    <router-link :to="`/movies/${currentMovie.id}/edit`">Edit</router-link><br>
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      currentMovie: {}
    };
  },
  created: function() {
    axios.get(`/api/movies/${this.$route.params.id}`).then(response => {
      console.log(response.data);
      this.currentMovie = response.data;
    });
  },
  methods: {}
};
</script>