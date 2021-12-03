<template>
  <header>
    <h1>
      BOOLFIX
    </h1>
    <nav>
      <input type="text" placeholder="Search" v-model="query" />
      <button @click.prevent="getArray">Search</button>
    </nav>
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
      listTv: [],
      apiUrlFilm:
        "https://api.themoviedb.org/3/search/movie?api_key=bd6af5f27de039c66efea1f8e2b13067&language=en-US&page=1&include_adult=false",
      apiUrlTv: 
        "https://api.themoviedb.org/3/search/tv?api_key=bd6af5f27de039c66efea1f8e2b13067&language=en-US&page=1&include_adult=false",
    };
  },
  methods: {
    // funzione che mi ritorna l'array di film e serie tv
    getArray() {
      // chiamata axios che mi torna i film
      Axios.get(`${this.apiUrlFilm}&query=${this.query}`).then((res) => {
        this.listFilm = res.data.results;
        console.log("axios mi torna questi film:", this.listFilm);
        this.$emit("searchFilm", this.listFilm);
      });

      // https://api.themoviedb.org/3/search/tv?api_key=bd6af5f27de039c66efea1f8e2b13067&language=en-US&page=1&include_adult=false
      // chiamata axios che mi torna i le serie tv
      Axios.get(`${this.apiUrlTv}&query=${this.query}`).then((res) => {
        this.listTv = res.data.results;
        console.log("axios mi torna queste serie tv:", this.listTv);
        this.$emit("searchTv", this.listTv);
      });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  header {
    height: 80px;
    display: flex;
    justify-content: space-between;
    align-items: center;

    h1 {
      color: red;
      margin: 0 20px;
    }

    nav {
      margin: 0 20px;
      color: white;
      & input {
        height: 30px;
        padding: 0 5px;
      }

      & button {
        height: 30px;
        padding: 0 3px;
      }
    }
  }
</style>
