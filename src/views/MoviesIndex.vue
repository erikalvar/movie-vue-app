<template>
  <div class="movies-index">
    
    <!-- <h1>{{ message }}</h1>
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
    </div> -->


    <div class="wrapper row3">
  <main class="hoc container clear"> 
    <!-- main body -->
    <!-- ################################################################################################ -->
    <div class="btmspace-50 center">
      <h3 class="btmspace-10">All Movies</h3>
      <p class="nospace">Click on the box for more info</p>
      <p>Search by title: <input v-model="titleFilter"></p>
      <div>
        <button>Sort Alphabetically</button>
      </div>
    </div>
    <ul class="nospace clear services">
      <div v-for="movie in orderBy(filterBy(movies, titleFilter, 'title'), 'title')">

        <li class="one_quarter first"><a href="#">
          <figure><img src="https://image.flaticon.com/icons/svg/54/54335.svg" alt="">
            <figcaption>{{ movie.title }}</figcaption>
            <router-link v-bind:to="`/movies/${movie.id}`">Show Info</router-link>
          </figure>
          </a>
        </li>
      </div> 
      
    </ul>
    <p class="center"><a class="btn inverse" href="#">Show More</a></p>
    <!-- ################################################################################################ -->
    <!-- / main body -->
    <div class="clear"></div>
  </main>
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