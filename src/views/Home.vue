<template>
  <div class="home">
    <img
      src="https://images.unsplash.com/photo-1539481915544-f5cd50562d66?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=728&q=80"
      alt="Movie Theatre Marquee"
      width="600"
      height="600"
    />
    <h1 style="background-color: rgb(106, 90, 205)">Movies</h1>
    <div v-for="movie in movies" v-bind:key="movie.id">
      <h2>Movie: {{ movie.title }} {{ movie.year }}</h2>
    </div>
    <!-- <div>
      Title:
      <input type="text" v-model="newMovieParams.title" />
    </div>
    <div>
      Year:
      <input type="text" v-model="newMovieParams.year" />
    </div> -->
    <button type="button" v-on:click="createMovie()" class="btn btn-success">Create Movie</button>
    <!-- <button v-on:click="createMovie()">Create Movie</button> -->
  </div>
</template>

<style>
/* body {
  background-image: url("https://images.unsplash.com/photo-1539481915544-f5cd50562d66?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=728&q=80");
} */
</style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      movies: [],
      newMovieParams: {},
    };
  },
  created: function () {
    this.indexMovies();
  },
  methods: {
    indexMovies: function () {
      axios.get("http://localhost:3000/movies").then((response) => {
        console.log(response.data);
        this.movies = response.data;
      });
    },
    createMovie: function () {
      var params = {
        title: "Waiting to Exhale",
        year: 1999,
      };
      axios.post("http://localhost:3000/movies", params).then((response) => {
        console.log(response.data);
        this.movies.push = response.data;
      });
    },
  },
};
</script>
