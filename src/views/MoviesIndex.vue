<template>
  <div class="home">
    <h1>Movies</h1>
    <div>
      <button v-on:click="sortAttribute">Sort Alphabetically</button>
    </div>
    <!-- views/MoviesIndex.vue
    <div v-for="movie in orderBy(filterBy(movies, titleFilter, 'title'), 'title')" v-bind:key="movie.id"></div> -->

    Search by name:
    <input v-model="titleFilter" list="titles" />
    <datalist id="titles">
      <option v-for="movie in movies" v-bind:key="movie.id">{{ movie.title }}</option>
    </datalist>
    Search by title:
    <input v-model="titleFilter" />
    <div v-for="movie in orderBy(filterBy(movies, titleFilter, 'title'), sortAttribute)" v-bind:key="movie.id">
      <h2>Movie: {{ movie.title }} {{ movie.year }}</h2>
      <router-link :to="`/movies/${movie.id}`">See Details</router-link>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: function () {
    return {
      movies: [],
      titleFilter: "",
      sortAttribute: "title",
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
