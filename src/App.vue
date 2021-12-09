<template>
  <div id="app">
    <div id="bg-header">
      <MyHeader @search="saveValue"/>
    </div>
    <div id="bg-main">
      <MyMain :query="valueForSearch"/>    
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
      valueForSearch: null,
    }
  },
  methods: {
    saveValue(val){
      this.valueForSearch = val
      console.log("il valore che mi torna l'header:",this.valueForSearch);
    },
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
