<template>
  <main>
    <!-- film -->
    <div class="container-card" v-for="film in listFilm" :key="film.id">
      <div class="card">
        <div class="cover">
          <img v-if="film.poster_path !== null" :src="coverUrl + film.poster_path" :alt="film.title" />
          <img v-else class="cover-netflix" src="https://i.pinimg.com/564x/01/e1/35/01e135a5bcabe81ce279076de8dfbfd9.jpg" alt="">
          
          <!-- container info -->
          <div class="container-info">
            <div>Titolo: {{ film.title }}</div>
            <div>Titolo Originale: {{ film.original_title }}</div>
            <div class="language">Lingua: <img :src="insertFlag(film.original_language)" /></div>

            <!-- contenitore del voto -->
            <div>
              Voto:
              <span v-for="star, i in addStars(film)" :key="i">
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
              Voto:
              <span v-for="star, i in addStars(tv)" :key="i">
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
import {EventBus} from '@/EventBus.js'
import Axios from 'axios'
export default {
  name: "MyMain",
  props: {
    // query:String
  },
  data() {
    return {
      listFilm: [],
      listTv: [],
      apiUrlFilm:
        "https://api.themoviedb.org/3/search/movie?api_key=bd6af5f27de039c66efea1f8e2b13067&language=en-US&page=1&include_adult=false",
      apiUrlTv: 
        "https://api.themoviedb.org/3/search/tv?api_key=bd6af5f27de039c66efea1f8e2b13067&language=en-US&page=1&include_adult=false",
      itFlag: require("@/assets/it_flag.png"),
      enFlag: require("@/assets/en_flag.png"),
      frFlag: require("@/assets/fr_flag.png"),
      coverUrl: "http://image.tmdb.org/t/p/w342",
    };
  },
  created(){
    EventBus.$on('search', this.getArray)
  },
  methods: {
    // funzione che mi ritorna l'array di film e serie tv
    getArray(queryFromSearch) {
      // chiamata axios che mi torna i film
      Axios.get(`${this.apiUrlFilm}&query=${queryFromSearch}`).then((res) => {
        this.listFilm = res.data.results;
        console.log("axios mi torna questi film:", this.listFilm);
        // this.$emit("searchFilm", this.listFilm);
      });

      // https://api.themoviedb.org/3/search/tv?api_key=bd6af5f27de039c66efea1f8e2b13067&language=en-US&page=1&include_adult=false
      // chiamata axios che mi torna i le serie tv
      Axios.get(`${this.apiUrlTv}&query=${queryFromSearch}`).then((res) => {
        this.listTv = res.data.results;
        console.log("axios mi torna queste serie tv:", this.listTv);
        // this.$emit("searchTv", this.listTv);
      });
    },

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
    addStars(item){
      let arrayStar = [];
      for (let i = 0; i < 5; i++){
        if (i > (item.vote_average / 2) - 1){
          arrayStar.push("far fa-star");
        } else {
          arrayStar.push("fas fa-star");
        }
      }
        return arrayStar
    }
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
main {
  display: flex;
  align-items: stretch;
  margin: 0px auto;
  width: 70%;
  display: flex;
  flex-wrap: wrap;
}

.container-card {
  width: calc(100% / 3);
  margin: 20px 0;
  color: white;
}

.card {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;

  .cover  {
    background-color: black;
    height: 500px;
    cursor: pointer;

    &:hover img {
      display: none;
    }

    &:hover .container-info {
      display: block;
    }
  }

  .language img {
    height: 10px;
  }
}

.container-info {
  display: none;
  width: 342px;
}

.cover img {
  height: 100%;
}

// .cover:hover .container-info {
//     display: block;
// }
.cover:hover img {
    display: none;
  }

.cover-netflix {
  width: 342px;
}

.star {
  color: yellow;
}

</style>
