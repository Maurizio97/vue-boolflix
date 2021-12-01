<template>
  <main>
      <!-- <div class="container-card">
          <div class="card">

          </div>
      </div> -->
      <ul>
          <!-- <li v-for="film, i in listFilm" :key="i">
              {{film.result.original_title}}
          </li> -->
      </ul>
  </main>
</template>

<script>
import Axios from 'axios'
export default {
  name: 'MyMain',
  data(){
      return {
          listFilm: [],
          apiUrl:"https://api.themoviedb.org/3/search/movie?api_key=bd6af5f27de039c66efea1f8e2b13067",
          query:"hitman",
      }
  },
  created() {
      this.getArray()
      
  },
  methods: {
    //   https://api.themoviedb.org/3/search/movie?api_key=bd6af5f27de039c66efea1f8e2b13067&query=Ritorno+al+futuro&language=en-US&page=1&include_adult=false
    // https://api.themoviedb.org/3/search/movie?api_key=bd6af5f27de039c66efea1f8e2b13067&query=hitman
      getArray(){
          Axios
        // .get("https://api.themoviedb.org/3/search/movie?api_key=bd6af5f27de039c66efea1f8e2b13067&query=hitman")
          .get(`${this.apiUrl}&query=${this.query}`)
          .then((res) => {
              this.listFilm = res;
              console.log("axios mi torna:",this.listFilm);
            })
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
    main {
        margin: 0 auto;
        width: 70%;
    }
    .container-card {
        // debug
        height: 200px;
        width: 100px;
        background-color: blueviolet;
    }
</style>
