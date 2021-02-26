<template>
  <div class="movies-show">
    <div class="jumbotron">
      <h1 class="display-4">{{ movie.title }}</h1>
      <h5 class="display-8">Directed By: {{ movie.director }} | {{ movie.year }} | English: {{ movie.english }}</h5>
      <img class="mb-3" :src="movie.poster" alt="" />
      <p class="lead">
        {{ movie.plot }}
      </p>
      <hr class="my-4" />
      <p><b>Genres:</b></p>
      <div v-for="genre in movie.genres" :key="genre.id">
        <p>{{ genre }}</p>
      </div>
      <router-link to="/movies" custom v-slot="{ navigate }">
        <span class="btn btn-outline-primary" @click="navigate" @keypress.enter="navigate" role="link">
          Back
        </span>
      </router-link>
      <router-link :to="`/movies/${this.movie.id}/edit`" custom v-slot="{ navigate }">
        <span class="btn btn-outline-primary ml-1" @click="navigate" @keypress.enter="navigate" role="link">
          Edit Movie
        </span>
      </router-link>
    </div>
    <div class="row">
      <div class="card mb-3 mx-auto" style="max-width: 900px;" v-for="actors in movie.actors" :key="actors.id">
        <div class="row no-gutters">
          <div class="col-md-4">
            <img :src="actors.photo" class="card-img" alt="..." />
          </div>
          <div class="col-md-7">
            <div class="card-body">
              <h1 class="card-title">{{ actors.first_name }} {{ actors.last_name }}</h1>
              <h6 class="card-text mb-4">Age: {{ actors.age }} | {{ actors.gender }}</h6>
              <h5 class="card-text">Best Known For: {{ actors.known_for }}</h5>
              <p class="card-text">
                {{ actors.movie_plot }}
              </p>
              <p class="card-text"><small class="text-muted">Last updated 3 mins ago</small></p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      movie: {},
    };
  },
  created: function() {
    axios.get(`/api/movies/${this.$route.params.id}`).then(response => {
      console.log(response.data);
      this.movie = response.data;
    });
  },
  methods: {},
};
</script>
