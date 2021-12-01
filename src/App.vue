<template>
  <div id="app">
    <MyHeader @search="saveArrayFilms"/>
    <MyMain :details="ArrayFilmsFromSearch"/>
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
    }
  },
  methods: {
    saveArrayFilms(val){
      this.ArrayFilmsFromSearch = val
      console.log("array dall'header",this.ArrayFilmsFromSearch);
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
</style>
