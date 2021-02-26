<template>
  <div id="app">
    <div id="nav">
      <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
        <a class="navbar-brand" href="#">Movie App</a>
        <button
          class="navbar-toggler"
          type="button"
          data-toggle="collapse"
          data-target="#navbarNav"
          aria-controls="navbarNav"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav ml-auto">
            <li class="nav-item">
              <router-link class="nav-link" to="/">Home</router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link" to="/movies">All Movies</router-link>
            </li>
            <li v-if="isLoggedIn()" class="nav-item">
              <router-link class="nav-link" to="/movies/new">New Movie</router-link>
            </li>
            <li v-if="!isLoggedIn()" class="nav-item">
              <router-link class="nav-link" to="/signup">Sign Up</router-link>
            </li>
            <li v-if="!isLoggedIn()" class="nav-item">
              <router-link class="nav-link" to="/login">Log In</router-link>
            </li>
            <li v-if="isLoggedIn()" class="nav-item">
              <router-link class="nav-link" to="/logout">Logout</router-link>
            </li>
          </ul>
        </div>
      </nav>
      <!-- <router-link to="/">Home</router-link>
      <span v-if="!isLoggedIn()">
        |
        <router-link to="/signup">Signup</router-link>
        |
        <router-link to="/login">Login</router-link>
      </span>
      <span v-else>
        |
        <router-link to="/logout">Logout</router-link>
      </span>
      |
      <router-link to="/movies">Movies Index</router-link>
      |
      <router-link to="/movies/new">Add Movie</router-link> -->
    </div>
    <router-view />
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
</style>

<script>
export default {
  methods: {
    isLoggedIn: function() {
      return localStorage.getItem("jwt");
    },
  },
};
</script>
