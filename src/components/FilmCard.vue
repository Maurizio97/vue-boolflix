<template>
  <div>
    <!-- film -->
    <div class="container-card" v-for="film in ArraylistFilm" :key="film.id">
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
  </div>
</template>

<script>
export default {
  name: "FilmsCard",
  props: {
    listFilm:Array
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>
