<template>

    <!-- poster_path -->
    <div class="container-card">
      <div class="card">
        <div class="cover">
          <img v-if="object.poster_path !== null" :src="coverUrl + object.poster_path" :alt="object.title" />
          <img v-else class="cover-netflix" src="https://i.pinimg.com/564x/01/e1/35/01e135a5bcabe81ce279076de8dfbfd9.jpg" alt="cover standard">
          
          <!-- container info -->
          <div class="container-info">
            <div>Titolo: {{ object.title? object.title: object.name }}</div>
            <div>Titolo Originale: {{ object.original_title? object.original_title: object.original_name }}</div>
            <div class="language">Lingua: <img :src="insertFlag(object.original_language)" /></div>
            <!-- qui stampo il cast -->
            <div>
              Cast: 
              <span v-for="item,i in object.cast" :key="i">
                {{ item.name }},
              </span> 
            </div>
            <!-- contenitore del voto -->
            <div>
              Voto:
              <span v-for="star, i in addStars(object)" :key="i">
                <i class="star" :class="star"></i>
              </span>
            </div>
            <!-- //contenitore del voto -->

          </div>

        </div>
      </div>
    </div>
</template>

<script>
export default {
  name: 'Card',
  props: {
    objectFilm:Object,
    objectTv:Object,
  },
  data() {
      return {
        itFlag: require("@/assets/it_flag.png"),
        enFlag: require("@/assets/en_flag.png"),
        frFlag: require("@/assets/fr_flag.png"),
        coverUrl: "http://image.tmdb.org/t/p/w342",
      }
  },
  computed: {
    object(){
        if(this.objectFilm){
          return this.objectFilm;
        } 
        return this.objectTv;
    },
    
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
    // funzione per aggiungere le stelle
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
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
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

    .language img {
    height: 10px;
    display: inline-block;
    }
  }

  .language img {
    height: 10px;
    display: block;
  }
}

.container-info {
  display: none;
  width: 342px;
}

.cover img {
  height: 100%;
}

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
