<template>
  <header>
    <h1>
      BOOLFIX
    </h1>
    <nav>
      <input type="text" placeholder="Search" v-model="query" />
      <button @click.prevent="saveValueInBus()">Search</button>
    </nav>
  </header>
</template>

<script>
import {EventBus} from '@/EventBus.js'
// import Axios from "axios";
export default {
  name: "MyHeader",
  data() {
    return {
      query: "",
    };
  },
  methods: {
    saveValueInBus(){
      EventBus.$emit('search', this.query )
    }
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  header {
    height: 80px;
    display: flex;
    justify-content: space-between;
    align-items: center;

    h1 {
      color: red;
      margin: 0 20px;
    }

    nav {
      margin: 0 20px;
      color: white;
      & input {
        height: 30px;
        padding: 0 5px;
      }

      & button {
        height: 30px;
        padding: 0 3px;
      }
    }
  }
</style>
