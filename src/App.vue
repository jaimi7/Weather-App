<template>
  <div id="app">
    <HomeComp />
  </div>
</template>

<script>
import HomeComp from './components/HomeComp.vue'

export default {
  name: "App",
  components:{
HomeComp
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
