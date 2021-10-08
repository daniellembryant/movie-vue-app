<template>
  <div class="home">
    <h1>Movies</h1>
    <div v-for="movie in movies" v-bind:key="movie.id">
      <h2>Movie: {{ movie.title }} {{ movie.year }}</h2>
      <router-link :to="`/movies/${movie.id}`">See Details</router-link>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      movies: [],
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
  },
};
</script>
