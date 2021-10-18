<template>
  <div class="movies-new">
    <form v-on:submit.prevent="createMovie()">
      <h1 style="background-color: rgb(106, 90, 205)">New Movie</h1>
      <img
        src="https://images.unsplash.com/photo-1440404653325-ab127d49abc1?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1170&q=80
      "
        alt="Movie projector"
        width="600"
        height="600"
      />
      <ul>
        <li v-for="error in errors" v-bind:key="error" {{ error }}></li>
      </ul>
      <div>
        <label>Title:</label>
        <input type="text" v-model="newMovieParams.title" />
      </div>
      <div>
        <label>Year:</label>
        <input type="text" v-model="newMovieParams.year" />
      </div>
      <div>
        <label>Plot:</label>
        <input type="text" v-model="newMovieParams.plot" />
        <br />
        <small>{{ 100 - newMovieParams.plot.length }} characters remaining</small>
        <p>{{ newMovieParams }}</p>
      </div>
      <input type="submit" value="Create" />
    </form>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      newMovieParams: {
        plot: "",
      },
      errors: [],
    };
  },
  methods: {
    createMovie: function () {
      axios
        .post("/movies", this.newMovieParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/movies");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
