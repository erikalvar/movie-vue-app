<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div v-for="movie in movies">
      <h3>{{ movie.title }}</h3>
      <button v-on:click=showMovie(movie)>More Info</button>
    </div>

    <dialog id="movie-info">
      <form method="dialog">
        <h1>Movie Info</h1>
        <p>Title: <input type="text" v-model="currentMovie.title"></p>
        <p>Year: <input type="text" v-model="currentMovie.year"></p>
        <p>Plot: <input type="text" v-model="currentMovie.plot"></p>
        <p>Director: <input type="text" v-model="currentMovie.director"></p>
        <!-- <p>English: <input type="text" v-model="currentMovie.english"></p> -->
        <button v-on:click="updateMovie(currentMovie)">Update</button>
        <button v-on:click="destroyMovie(currentMovie)"> Delete</button>
        <button>Close</button>
      </form>
    </dialog>

    <div>
      <h1>Add New Movie</h1>
      <p>Title: <input type="text" v-model="newMovieTitle"></p>
      <p>Year: <input type="text" v-model="newMovieYear"></p>
      <p>Plot: <input type="text" v-model="newMoviePlot"></p>
      <p>Director: <input type="text" v-model="newMovieDirector"></p>
      <!-- <p>English: <select v-model="selected">
        <option v-for="option in options" v-bind:value="option.value">
        {{ option.text }}
        </option>
      </select></p> -->
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
      message: "Movies Index",
      movies: [],
      newMovieTitle: "",
      newMovieYear: "",
      newMoviePlot: "",
      newMovieDirector: "",
      // newMovieEnglish: "",
      // options: [
      //   { text: "True", value: "true" },
      //   { text: "False", value: "false" }
      // ],
      currentMovie: {}
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
    },
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
        .catch(error => {
          console.log(error.response.data.errors);
          this.errors = error.response.data.errors;
        });
    },
    showMovie: function(movie) {
      console.log(movie);
      this.currentMovie = movie;
      document.querySelector("#movie-info").showModal();
    },
    updateMovie: function(movie) {
      var params = {
        title: movie.title,
        year: movie.year,
        plot: movie.plot,
        director: movie.director
        // english: movie.english
      };
      axios.patch(`/api/movies/${movie.id}`, params).then(response => {
        console.log("Successfully Updates", response.data);
      });
    },
    destroyMovie: function(movie) {
      axios.delete(`/api/movies/${movie.id}`).then(response => {
        console.log("Successfully Deleted", response.data);
        var index = this.movies.indexOf(movie);
        this.movies.splice(index, 1);
      });
    }
  }
};
</script>