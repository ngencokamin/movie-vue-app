<template>
  <div class="home">
    <button class="add" v-on:click="showAdd = !showAdd">Add Movie</button>

    <!-- <button class="login" v-if="!loggedIn" v-on:click="showLogin = !showLogin">Login</button>
    <button class="login" v-if="loggedIn" v-on:click="logoff">Sign Out</button> -->

    <br>

    <!-- <button class="login" v-if="showLogin" v-on:click="login">Sign in</button>
    <input class="login" v-if="showLogin" v-model="password" type="text" placeholder="Password">
    <input class="login" v-if="showLogin" v-model="email" type="text" placeholder="Email"> -->

    <input class="add" v-if="showAdd" v-model="title" type="text" placeholder="Title">
    <input class="add" v-if="showAdd" v-model.number="year" type="number" placeholder="Year">
    <br v-if="showAdd">
    <input class="add" v-if="showAdd" v-model="director" type="text" placeholder="Director">
    <textarea v-model="plot" class="add" v-if="showAdd" placeholder="Movie plot"></textarea>
    <br v-if="showAdd">
    <br v-if="showAdd">
    <input type="checkbox" class="add" v-if="showAdd" id="checkbox" v-model="english">
    <label class="add" v-if="showAdd" for="checkbox">English?</label>
    <button class="add" v-if="showAdd" v-on:click="addMovie">Add</button>


    
    <h1>Movies</h1>
    <div v-for="movie in movies" :key="movie.id">
      <h2> {{ movie.title }} </h2>
      <p> {{ movie.director }} | {{ movie.year }} | English: {{ movie.english }}</p>
      <p> {{ movie.plot }}</p>
      <p>Genres:</p>
      <div v-for="genre in movie.genres" :key="genre.id">
        <p><b> {{ genre }} </b></p>
      </div>
    </div>
  </div>
</template>
<style>
/* .login {
  float: right;
} */
.add {
  float:left;
}
</style>
<script>
import axios from "axios"
export default {
  data: function() {
    return {
      message: "Welcome to Vue.js!",
      // loggedIn: false,
      // showLogin: false,
      // email: "",
      // password: "",
      // token: "",
      movies: [],
      showAdd: false,
      title: "",
      english: false,
      director: "",
      year: null,
      plot: ""
    };
  },
  created: function() {
    this.moviesIndex();
  },
  methods: {
    // login: function() {
    //   var params = {
    //     email: this.email,
    //     password: this.password
    //   }
    //   axios.post("/api/sessions", params)
    //   .then((response) => {
    //     this.token = response.data.jwt;
    //   })
    //   .catch((error) => {
    //     console.log(error.response.data.errors)
    //   });
    //   this.loggedIn = true;
    //   this.showLogin = false;
    // },
    // logoff: function() {
    //   this.loggedIn = false;
    //   this.token = "";
    //   this.email = "";
    //   this.password = "";
    // },
    moviesIndex: function() {
      axios.get("/api/movies")
      .then(response => {
        console.log(response.data);
        this.movies = (response.data);
      })
      .catch((error) => {
        console.log(error.response.data.errors)
      });
    },
    addMovie: function() {
      var params = {
        title: this.title,
        english: this.english,
        director: this.director,
        year: this.year,
        plot: this.plot
      }
      axios.post("/api/movies", params)
      .then((response) => {
        console.log(response.data);
        this.movies.push(response.data);
      })
      .catch((error) => {
        console.log(error.response.data.errors)
      });
    }
  }
};
</script>