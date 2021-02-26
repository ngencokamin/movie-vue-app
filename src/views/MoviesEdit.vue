<template>
  <div class="movies-new">
    <form v-on:submit.prevent="updateMovie()">
      <h1>Edit Movie</h1>
      <ul>
        <li class="text-danger" v-for="error in errors" v-bind:key="error">
          {{ error }}
        </li>
      </ul>
      <div class="form-group">
        <label>Title:</label>
        <input type="text" class="form-control" v-model="movie.title" />
      </div>
      <div class="form-group">
        <label>Year:</label>
        <input type="number" class="form-control" v-model.number="movie.year" />
      </div>
      <div class="form-group">
        <label>Director:</label>
        <input type="text" class="form-control" v-model="movie.director" />
      </div>
      <div class="form-group">
        <label>Poster URL:</label>
        <input type="text" class="form-control" v-model="movie.poster" />
      </div>
      <label>Plot:</label>
      <div class="form-group">
        <textarea name="plot" v-model="movie.plot" placeholder="Plot" cols="30" rows="10"></textarea>
      </div>
      <div class="form-group">
        <input type="checkbox" id="checkbox" v-model="movie.english" />
        <label for="checkbox">English?</label>
      </div>
      <div class="form-group"></div>
      <input type="submit" class="btn btn-outline-primary mr-1" value="Update" />
      <button type="button" class="btn btn-outline-warning" data-toggle="modal" data-target="#deleteModal">
        Delete Movie
      </button>
    </form>

    <!-- Modal -->
    <div class="modal fade" id="deleteModal" tabindex="-1" aria-labelledby="deleteModalLabel" aria-hidden="true">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLabel">Confirm Deletion</h5>
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="modal-body">Are you sure you want to delete "{{ movie.title }}"?</div>
          <div class="modal-footer">
            <button type="button" class="btn btn-outline-secondary" data-dismiss="modal">Cancel</button>
            <button type="button" v-on:click="destroyMovie()" class="btn btn-danger" data-dismiss="modal">
              Confirm Deletion
            </button>
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
      errors: [],
    };
  },
  created: function() {
    axios.get(`/api/movies/${this.$route.params.id}`).then(response => {
      console.log(response.data);
      this.movie = response.data;
    });
  },
  methods: {
    updateMovie: function() {
      var params = {
        title: this.movie.title,
        year: this.movie.year,
        plot: this.movie.plot,
        director: this.movie.director,
        english: this.movie.english,
        poster: this.movie.poster,
      };

      axios
        .patch(`/api/movies/${this.movie.id}`, params)
        .then(response => {
          console.log(response.data);
          this.$router.push(`/movies/${this.movie.id}`);
        })
        .catch(error => {
          console.log(error.response);
          this.errors.push(error.response.status + " " + error.response.statusText);
        });
    },
    destroyMovie: function() {
      axios
        .delete(`/api/movies/${this.movie.id}`)
        .then(response => {
          console.log(response.data);
          alert(response.data.message);
          this.$router.push("/movies");
        })
        .catch(error => {
          this.errors = error.response.data.errors;
          alert("Error! Couldn't delete post");
        });
    },
  },
};
</script>
