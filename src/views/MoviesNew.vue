<template>
  <div class="movies-new">
    <form v-on:submit.prevent="addMovie()">
      <h1>New Movie</h1>
      <ul>
        <li class="text-danger" v-for="error in errors" v-bind:key="error">
          {{ error }}
        </li>
      </ul>
      <div class="form-group">
        <label>Title:</label>
        <input type="text" class="form-control" v-model="title" />
      </div>
      <div class="form-group">
        <label>Year:</label>
        <input type="number" class="form-control" v-model.number="year" />
      </div>
      <div class="form-group">
        <label>Director:</label>
        <input type="text" class="form-control" v-model="director" />
      </div>
      <div class="form-group">
        <textarea name="plot" v-model="plot" placeholder="Plot" cols="30" rows="10" maxlength="500"></textarea>
      </div>
      <small>{{ plotLength - plot.length }} characters remaining</small>
      <div class="form-group">
        <input type="checkbox" id="checkbox" v-model="english" />
        <label for="checkbox">English?</label>
      </div>
      <div class="form-group"></div>
      <input type="submit" class="btn btn-primary" value="Create Movie" />
    </form>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      title: "",
      year: "",
      plot: "",
      director: "",
      english: false,
      errors: [],
      plotLength: 500,
    };
  },
  created: function() {},
  methods: {
    addMovie: function() {
      var params = {
        title: this.title,
        year: this.year,
        plot: this.plot,
        director: this.director,
        english: this.english,
      };

      axios
        .post("/api/movies", params)
        .then(response => {
          console.log(response.data);
          this.$router.push("/movies");
        })
        .catch(error => {
          console.log(error.response);
          this.errors.push(error.response.status + " " + error.response.statusText);
        });
    },
  },
};
</script>
