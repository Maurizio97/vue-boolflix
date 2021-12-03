<template>
  <main>
    <!-- film -->
    <div class="container-card" v-for="film in listFilm" :key="film.id">
      <div class="card">
        <div class="cover">
          <!-- <img v-if="film.poster_path !== null" :src="coverUrl + film.poster_path" :alt="film.title" />
          <img v-else class="cover-netflix" src="https://i.pinimg.com/564x/01/e1/35/01e135a5bcabe81ce279076de8dfbfd9.jpg" alt=""> -->
          
          <!-- container info -->
          <div class="container-info">
            <div>Titolo: {{ film.title }}</div>
            <div>Titolo Originale: {{ film.original_title }}</div>
            <div class="language">Lingua: <img :src="insertFlag(film.original_language)" /></div>

            <!-- contenitore del voto -->
            <div>
              <span v-for="star, i in arrayStar" :key="i" :class="i > (film.vote_average / 2) - 1? 'none': ''">
                <i class="star" :class="star"></i>
              </span>
            </div>
            <!-- //contenitore del voto -->

          </div>

        </div>
      </div>
    </div>
    <!-- serie tv -->
    <!-- poster_path -->
    <div class="container-card" v-for="tv in listTv" :key="tv.id">
      <div class="card">
        <div class="cover">
          <img class="cover-img" v-if="tv.poster_path !== null" :src="coverUrl + tv.poster_path" :alt="tv.title" />
          <img v-else class="cover-netflix" src="https://i.pinimg.com/564x/01/e1/35/01e135a5bcabe81ce279076de8dfbfd9.jpg" alt="">
          
          <!-- container info -->
          <div class="container-info">
            <div>Titolo: {{ tv.title }}</div>
            <div>Titolo Originale: {{ tv.original_title }}</div>
            <div class="language">Lingua: <img :src="insertFlag(tv.original_language)" /></div>

            <!-- contenitore del voto -->
            <div>
              <span v-for="star, i in arrayStar" :key="i" :class="i > (tv.vote_average / 2) - 1? 'none': ''">
                <i class="star" :class="star"></i>
              </span>
            </div>
            <!-- //contenitore del voto -->
          </div>

        </div>
      </div>
    </div>
  </main>
</template>

<script>
// import Axios from 'axios'
export default {
  name: "MyMain",
  props: {
    listFilm: Array,
    listTv: Array,
  },
  data() {
    return {
      itFlag: require("@/assets/it_flag.png"),
      enFlag: require("@/assets/en_flag.png"),
      frFlag: require("@/assets/fr_flag.png"),
      coverUrl: "http://image.tmdb.org/t/p/w342",
      arrayStar: [
        'fas fa-star',
        'fas fa-star',
        'fas fa-star',
        'fas fa-star',
        'fas fa-star',
      ]
    };
  },
  methods: {
    // funzione per aggiungere le bandiere
    insertFlag(item) {
      if (item === "it") {
        return this.itFlag;
      } else if (item === "en") {
        return this.enFlag;
      } else if (item === "fr") {
        return this.frFlag;
      } else {
        return "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQvUgkbNyXbD7bXamCmiGz2ZBAVbyaU_fvARQ&usqp=CAU";
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
main {
  display: flex;
  align-items: stretch;
  margin: 20px auto;
  width: 70%;
  display: flex;
  flex-wrap: wrap;
  background-color: grey;
}
.container-card {
  // padding: 20px;
  // debug
  // height: 200px;
  width: calc(100% / 3);
  margin-bottom: 20px;
  // background-color: #2c3e50;
  // border: 1px solid black;
  color: black;
}
.card {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100%;

  .language img {
    height: 10px;
  }
}

.container-info {
  // display: none;
}

.cover-img {
  height: 500px;
}

.cover-netflix {
  width: 342px;
  height: 100%;
}

.star {
  color: yellow;
}

.none {
  display: none;
}
</style>
