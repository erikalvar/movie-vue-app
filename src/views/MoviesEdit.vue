<template>
  <div class="movies-edit">
    <h1>{{ message }}</h1>
    <form v-on:submit.prevent="updateMovie()">
        <p>Title: <input type="text" v-model="currentMovie.title"></p>
        <p>Year: <input type="text" v-model="currentMovie.year"></p>
        <p>Plot: <input type="text" v-model="currentMovie.plot"></p>
        <p>Director: <input type="text" v-model="currentMovie.director"></p>
        <button v-on:click="updateMovie(currentMovie)">Update</button>
        <button v-on:click="destroyMovie(currentMovie)">Delete</button>
      </form>

  </div>
</template>

<style>
</style>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      message: "Edit Current Movie",
      currentMovie: {}
    };
  },
  created: function() {
    axios.get(`/api/movies/${this.$route.params.id}`).then(response => {
      console.log(response.data);
      this.currentMovie = response.data;
    });
  },
  methods: {
    updateMovie: function(movie) {
      var params = {
        title: this.currentMovie.title,
        year: this.currentMovie.year,
        plot: this.currentMovie.plot,
        director: this.currentMovie.director
      };
      axios
        .patch(`/api/movies/${this.currentMovie.id}`, params)
        .then(response => {
          console.log("Successfully Updates", response.data);
        });
    },
    destroyMovie: function(movie) {
      axios.delete(`/api/movies/${movie.id}`).then(response => {
        console.log("Successfully Deleted", response.data);
        var index = this.movies.indexOf(this.currentMovie);
        this.movies.splice(index, 1);
      });
    }
  }
};
</script>