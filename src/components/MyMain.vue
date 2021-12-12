<template>
  <main>
    <!-- card film -->
    <Card
    v-for="film in listFilm"
    :key="film.id"
    :objectFilm="film"
    />
    
    <!-- card serie tv -->
    <Card
    v-for="tv in listTv"
    :key="tv.id"
    :objectTv="tv"
    />
    
  </main>
</template>

<script>
import {EventBus} from '@/EventBus.js'
import Axios from 'axios'
import Card from './Card.vue'
export default {
  name: "MyMain",
  components: {
    Card,
  },
  data() {
    return {
      listFilm: [],
      listTv: [],
      apiUrlFilm:
        "https://api.themoviedb.org/3/search/movie?api_key=bd6af5f27de039c66efea1f8e2b13067&language=en-US&page=1&include_adult=false",
      apiUrlTv: 
        "https://api.themoviedb.org/3/search/tv?api_key=bd6af5f27de039c66efea1f8e2b13067&language=en-US&page=1&include_adult=false",
    };
  },
  created(){
    EventBus.$on('search', this.getArray);
  },
  methods: {
    // funzione che mi ritorna l'array di film e serie tv
    getArray(queryFromSearch) {
      // chiamata axios che mi torna i film
      Axios.get(`${this.apiUrlFilm}&query=${queryFromSearch}`).then((res) => {
        this.listFilm = res.data.results;
        console.log("axios mi torna questi film:", this.listFilm);
        this.getCastFilm(this.listFilm);
      });

      // chiamata axios che mi torna i le serie tv
      Axios.get(`${this.apiUrlTv}&query=${queryFromSearch}`).then((res) => {
        this.listTv = res.data.results;
        console.log("axios mi torna queste serie tv:", this.listTv);
      });
    },
    
    // async getCast(arr){

    //   const listId = arr.map(film => film.id);
    //   console.log(listId);
    //   console.log("lista id",listId);
    //   for( let id of listId){
    //     console.log("log for",id);
    //     const res = await Axios.get(`https://api.themoviedb.org/3/movie/${id}/credits?api_key=bd6af5f27de039c66efea1f8e2b13067&language=en-US`)
    //       this.listCast.push(res.data.cast); 
    //   }
    //     console.log(this.listCast);
    // },

    // funzione che mi aggiunge un array contente il cast (proveniente da una chiamata axios) all'array principale
    async getCastFilm(arr){
      for( let object of arr){
        console.log("log for",object.id);
        const res = await Axios.get(`https://api.themoviedb.org/3/movie/${object.id}/credits?api_key=bd6af5f27de039c66efea1f8e2b13067&language=en-US`)
          object.cast = res.data.cast;
      }
        console.log("after call",this.listFilm);
    },
  }
};
</script>

<style lang="scss">
main {
  display: flex;
  align-items: stretch;
  margin: 0px auto;
  width: 70%;
  display: flex;
  flex-wrap: wrap;
}
</style>