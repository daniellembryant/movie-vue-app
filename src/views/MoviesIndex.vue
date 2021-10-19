<template>
  <div class="home">
    <h1 style="background-color: rgb(106, 90, 205)">Movie List</h1>
    <img
      src="https://images.unsplash.com/photo-1626814026160-2237a95fc5a0?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1170&q=80"
      alt="Collection of movie posters"
      width="600"
      height="600"
    />

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
      <!-- cards -->
      <div class="card text-center mx-auto" style="width: 18rem">
        <router-link :to="`/movies/${movie.id}`">
          <img
            src="https://images.unsplash.com/photo-1542204165-65bf26472b9b?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1074&q=80"
            class="card-img-top"
            alt="..."
          />
        </router-link>
        <div class="card-body">
          <h5 class="card-title">{{ movie.title }}</h5>
          <p class="card-text">
            {{ movie.plot }}
          </p>
          <!-- <a href="#" class="btn btn-primary">See Details</a> -->
        </div>
      </div>
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
