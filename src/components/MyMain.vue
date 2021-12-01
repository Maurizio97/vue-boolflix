<template>
  <main>
      <div class="container-card" v-for="film, i in details" :key="i">
          <div class="card">
            <div> Titolo: {{film.title}}</div>
            <div>Titolo Originale: {{film.original_title}}</div>
            <div>Lingua: {{film.original_language}}</div>
            <div>Voto: {{film.vote_average}}</div>
          </div>
      </div>
      <!-- <ul>
          <li >
            <div>{{film.title}}</div>
            <div>{{film.original_title}}</div>
            <div>{{film.original_language}}</div>
            <div>{{film.vote_average}}</div>
          </li>
      </ul> -->
  </main>
</template>

<script>
// import Axios from 'axios'
export default {
  name: 'MyMain',
  props: {
      details:Array
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
