<template>
  <main>
      <div class="container-card" v-for="film, i in listFilm" :key="i">
          <div class="card">
            <div> Titolo: {{film.title}}</div>
            <div>Titolo Originale: {{film.original_title}}</div>
            <div>Lingua: {{film.original_language}}</div>
            <div>Voto: {{film.vote_average}}</div>
          </div>
      </div>
      <div class="container-card" v-for="tv in listTv" :key="tv.id">
          <div class="card">
            <div> Titolo: {{tv.name}}</div>
            <div>Titolo Originale: {{tv.original_name}}</div>
            <div>Lingua: {{tv.original_language}}</div>
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
        }
</style>
