<template>
  <header>
      <!-- debug -->
    <!-- $emit('search', $event.target.value) -->
    <!-- @click.prevent="$emit('search', inputValue)" -->
    <input type="text" placeholder="Search" v-model="query" />
    <button @click.prevent="getArray">Search</button>
  </header>
</template>

<script>
import Axios from "axios";
export default {
  name: "MyHeader",
  data() {
    return {
      query: "",
      listFilm: [],
      apiUrl:
        "https://api.themoviedb.org/3/search/movie?api_key=bd6af5f27de039c66efea1f8e2b13067",
    };
  },
  methods: {
    getArray() {
      Axios.get(`${this.apiUrl}&query=${this.query}`).then((res) => {
        this.listFilm = res.data.results;
        console.log("axios mi torna:", this.listFilm);
        this.$emit('search', this.listFilm)
      });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
</style>
