<template>
  <div>
    <input
      v-model="query"
      @keyup.enter="emitSearch"
      placeholder="Enter the movie title"
    />
    <button @click="emitSearch">Search</button>
  </div>
</template>

<script>
export default {
  props: {
    initialQuery: {
      type: String,
      default: "",
    },
  },
  data() {
    return {
      query: this.initialQuery,
    };
  },
  methods: {
    emitSearch() {
      if (this.query) {
        this.$emit("search", this.query);
        this.query = "";
      }
    },
  },
};
</script>

<style scoped>
div input {
  margin: 20px 0;
  padding: 10px 10px 10px 25px;
  width: 50%;
  border: 0;
  border-bottom: 2px solid rgb(0, 0, 0);
  outline: none;
  background-color: rgb(29, 29, 29);
  color: rgb(148, 136, 255);
  font-size: 18px;
}

div input:focus {
  border-bottom-color: violet;
}

div button {
  width: 15%;
  outline: none;
  padding: 10px;
  background-color: rgb(113, 113, 113);
  border: 0;
  font-size: 18px;
  transition: transform 0.2s ease;
}

div button:hover {
  transform: scale(0.95);
  background-color: violet;
}
</style>
