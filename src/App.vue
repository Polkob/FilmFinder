<template>
  <div class="wrapper">
    <h1>Film Finder</h1>
    <Input :initialQuery="query" @search="searchMovie" />

    <div v-if="movies.length > 0">
      <MovieList :movies="movies" />
    </div>

    <div v-else-if="searchPerformed">Movies not found</div>
  </div>
</template>

<script>
import axios from "axios";
import Input from "./components/Input.vue";
import MovieList from "./components/MovieList.vue";

export default {
  components: {
    Input,
    MovieList,
  },
  data() {
    return {
      movies: [],
      apiKey: "54a2541709252b5e3de68b7642666940",
      query: "",
      searchPerformed: false,
    };
  },
  computed: {
    imageUrl() {
      return (posterPath) => {
        return posterPath ? `https://image.tmdb.org/t/p/w500${posterPath}` : "";
      };
    },
  },
  methods: {
    searchMovie(query) {
      if (!query) return;

      axios
        .get(`https://api.themoviedb.org/3/search/movie`, {
          params: {
            api_key: this.apiKey,
            query: query,
          },
        })
        .then((response) => {
          const filteredMovies = response.data.results.filter(
            (movie) => movie.poster_path
          );
          if (filteredMovies.length > 0) {
            this.movies = filteredMovies.slice(0, 30);
            this.searchPerformed = true;
          } else {
            this.movies = [];
            this.searchPerformed = true;
          }
        })
        .catch((error) => {
          console.error("Error:", error);
        });
    },
  },
};
</script>

<style scoped>
.wrapper {
  background-color: black;
  width: 700px;
  min-height: 100vh;
  border-radius: 20px;
  margin: 20px;
  box-shadow: 0 2px 20px rgba(0, 0, 0, 0.4);
  color: rgb(148, 136, 255);
  font-family: "Montserrat", sans-serif;
  padding: 20px;
}
</style>
