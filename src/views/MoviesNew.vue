<template>
  <div class="movies-new">
    
    <div>
      <h1>Add New Movie</h1>
      <p>Title: <input type="text" v-model="newMovieTitle"></p>
      <p>Year: <input type="text" v-model="newMovieYear"></p>
      <p>Plot: <input type="text" v-model="newMoviePlot"></p>
      <p>Director: <input type="text" v-model="newMovieDirector"></p>
      <button v-on:click="createMovie()">Add</button>
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
      movies: [],
      newMovieTitle: "",
      newMovieYear: "",
      newMoviePlot: "",
      newMovieDirector: ""
    };
  },
  created: function() {},
  methods: {
    createMovie: function() {
      var params = {
        title: this.newMovieTitle,
        year: this.newMovieYear,
        plot: this.newMoviePlot,
        director: this.newMovieDirector,
        english: this.newMovieEnglish
      };

      axios
        .post("/api/movies", params)
        .then(response => {
          console.log("Success", response.data);
          this.movies.push(response.data);
        })
        .then(response => {
          this.$router.push("/movies");
        })
        .catch(error => {
          console.log(error.response.data.errors);
          this.errors = error.response.data.errors;
        });
    }
  }
};
</script>