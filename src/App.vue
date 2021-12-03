<template>
  <div id="app">
    <div id="bg-header">
      <MyHeader @searchFilm="saveArrayFilms" @searchTv="saveArrayTv"/>
    </div>
    <div id="bg-main">
      <MyMain :listFilm="ArrayFilmsFromSearch" :listTv="ArrayTvFromSearch"/>    
    </div>
  </div>
</template>

<script>
import MyHeader from './components/MyHeader.vue'
import MyMain from './components/MyMain.vue'

export default {
  name: 'App',
  components: {
    MyHeader,
    MyMain
  },
  data(){
    return {
      ArrayFilmsFromSearch: [],
      ArrayTvFromSearch: [],
    }
  },
  methods: {
    saveArrayFilms(val){
      this.ArrayFilmsFromSearch = val
      console.log("array dall'header film",this.ArrayFilmsFromSearch);
    },
    saveArrayTv(val){
      this.ArrayTvFromSearch = val
      console.log("array dall'header tv",this.ArrayTvFromSearch);
    }
  }
}
</script>

<style lang="scss">

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  // margin-top: 60px;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#bg-main {
  background-color: grey;
  min-height: calc(100vh - 80px);
}

#bg-header {
  background-color: black;
}
</style>
