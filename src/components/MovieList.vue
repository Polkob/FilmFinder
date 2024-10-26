<template>
  <div>
    <h2>Search results:</h2>
    <div class="movies-list">
      <div v-for="(movie, index) in movies" :key="index">
        <MovieItem :movie="movie" />
      </div>
    </div>
  </div>
</template>

<script>
import MovieItem from "./MovieItem.vue";

export default {
  components: {
    MovieItem,
  },
  props: {
    movies: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style scoped>
.movies-list {
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  justify-content: flex-start;
}

.movies-list > * {
  flex: 0 0 calc(33.33%);
  margin-top: 10px;
}
</style>
