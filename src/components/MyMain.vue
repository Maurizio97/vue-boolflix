<template>
  <main>
    <!-- film -->
      <div class="container-card" v-for="film in listFilm" :key="film.id">
          <div class="card">
            <div> Titolo: {{film.title}}</div>
            <div>Titolo Originale: {{film.original_title}}</div>
            <div>Lingua: <img :src="insertFlag(film.original_language)"></div>
            <div>Voto: {{film.vote_average}}</div>
          </div>
      </div>
      <!-- serie tv -->
      <div class="container-card" v-for="tv in listTv" :key="tv.id">
          <div class="card">
            <div> Titolo: {{tv.name}}</div>
            <div>Titolo Originale: {{tv.original_name}}</div>
            <div>Lingua: <img :src="insertFlag(tv.original_language)"></div>
            <div>Voto: {{tv.vote_average}}</div>
          </div>
      </div>
  </main>
</template>

<script>
// import Axios from 'axios'
export default {
  name: 'MyMain',
  props: {
      listFilm:Array,
      listTv:Array,
  },
  data(){
    return {
      itFlag: require("@/assets/it_flag.png"),
      enFlag: require("@/assets/en_flag.png"),
      frFlag: require("@/assets/fr_flag.png"),
    }
  },
  methods: {
    insertFlag(item){
      if(item === "it"){
        return this.itFlag
      } else if (item === "en"){
        return this.enFlag
      } else if (item === "fr"){
        return this.frFlag
      } else {
        return "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQvUgkbNyXbD7bXamCmiGz2ZBAVbyaU_fvARQ&usqp=CAU"
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
    main {
        margin: 20px auto;
        width: 70%;
        display: flex;
        flex-wrap: wrap;
    }
    .container-card {
        padding: 20px;
        // debug
        height: 200px;
        width: 20%;
        background-color: #2c3e50;
        border: 1px solid black;
        color: black;

        
    }
    .card {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100%;

            img {
              height: 10px;
            }
        }
</style>
