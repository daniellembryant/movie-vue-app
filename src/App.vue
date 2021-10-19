<template>
  <div id="app">
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <div class="container-fluid">
        <a class="navbar-brand" href="#">Navbar</a>
        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarSupportedContent"
          aria-controls="navbarSupportedContent"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarSupportedContent">
          <ul class="navbar-nav me-auto mb-2 mb-lg-0">
            <li class="nav-item">
              <router-link class="nav-link active" aria-current="page" to="/">Home</router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link" to="/about">About</router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link" to="/movies">Movies</router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link" to="/movies/new">Movie Create</router-link>
            </li>
            <li class="nav-item">
              <router-link v-if="!isLoggedIn()" class="nav-link" to="/signup">Signup</router-link>
            </li>
            <li class="nav-item">
              <router-link v-if="!isLoggedIn()" class="nav-link" to="/login">Login</router-link>
            </li>
            <li class="nav-item">
              <router-link v-if="isLoggedIn()" class="nav-link" to="/logout">Logout</router-link>
            </li>
          </ul>
          <form class="d-flex">
            <!-- original search bar -->
            <!-- <input v-model="titleFilter" list="titles" />
            <datalist id="titles">
              <option v-for="movie in movies" v-bind:key="movie.id">{{ movie.title }}</option>
            </datalist> -->
            <!-- Bootstrap Searchbar -->
            <input class="form-control me-2" type="search" placeholder="Search" aria-label="Search" />

            <button class="btn btn-outline-success" type="submit">Search</button>
          </form>
        </div>
      </div>
    </nav>
    <router-view />

    <!-- Search by name:
    <input v-model="titleFilter" list="titles" />
    <datalist id="titles">
      <option v-for="movie in movies" v-bind:key="movie.id">{{ movie.title }}</option>
    </datalist>
    Search by title:
    <input v-model="titleFilter" />
    <div v-for="movie in orderBy(filterBy(movies, titleFilter, 'title'), sortAttribute)" v-bind:key="movie.id">
      <h2>Movie: {{ movie.title }} {{ movie.year }}</h2> -->
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
<script>
export default {
  data: function () {
    return {
      flashMessage: "",
      titleFilter: "",
      sortAttribute: "title",
    };
  },
  methods: {
    isLoggedIn: function () {
      return localStorage.getItem("jwt");
    },
    getUserId: function () {
      return localStorage.user_id;
    },
  },
};
</script>
