<template>
  <div>
    <img
      v-if="movie.poster_path"
      :src="imageUrl(movie.poster_path)"
      :alt="movie.title + ' poster'"
    />
    <p v-else>Постер не найден</p>
    <h3>{{ movie.title }}</h3>
  </div>
</template>

<script>
export default {
  props: {
    movie: {
      type: Object,
      required: true,
    },
  },
  methods: {
    imageUrl(posterPath) {
      return posterPath ? `https://image.tmdb.org/t/p/w500${posterPath}` : "";
    },
  },
};
</script>

<style scoped>
div {
  width: 80%;
  max-height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 20px;
  padding-bottom: 10px;
  background-color: rgb(32, 32, 32);
}
div img {
  width: 100%;
  height: 70%;
}
div h3 {
  height: 40px;
  width: 100%;
  font-size: 13px;
  font-weight: 300;
  padding-top: 20px;
}
</style>
