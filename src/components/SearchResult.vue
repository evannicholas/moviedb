<template>
  <div class="row">
    <div class="col-6 col-lg-2" v-for="movie in movies" :key="movie.imdbID">
      <MovieThumb :movie="movie"></MovieThumb>
    </div>
  </div>
</template>

<script>
import { api } from "boot/axios";
import MovieThumb from "components/MovieThumb.vue";

export default {
  components: {
    MovieThumb,
  },
  props: {
    query: String,
  },
  data() {
    return {
      movies: [],
      countdown: -1,
    };
  },
  methods: {
    search() {
      console.log("Searching");
      api
        .get(`https://www.omdbapi.com/?apikey=57edaaef&r=json&s=${this.query}`)
        .then((response) => (this.movies = response.data.Search))
        .catch((error) => console.log(error));
    },
  },
  watch: {
    query(newValue, oldValue) {
    //   this.search();
        this.countdown = 1;
    },
  },
  mounted () {
      setInterval(() => {
          if (this.countdown > 0) {
              this.countdown--;
          } else if (this.countdown == 0) {
              this.search();
              this.countdown--;
          }
      }, 500);
  },
};
</script>

<style lang="scss" scoped>

</style>