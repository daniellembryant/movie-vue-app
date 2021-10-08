<template>
  <div class="movies-show">
    <h2>{{ currentMovie.title }}</h2>
    <p>Title: {{ currentMovie.title }}</p>
    <p>Year: {{ currentMovie.year }}</p>
    <p>Plot: {{ currentMovie.plot }}</p>
    <router-link :to="`/movies/${currentMovie.id}/edit`">Edit Movie</router-link>
  </div>
</template>

<style></style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      currentMovie: {},
    };
  },
  created: function () {
    axios.get(`/movies/${this.$route.params.id}`).then((response) => {
      console.log(response.data);
      this.currentMovie = response.data;
    });
  },
  methods: {},
};
</script>
