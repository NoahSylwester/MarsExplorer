<template>
  <div id="app">
    <Splash />
  </div>
</template>

<script>
import Splash from './components/Splash.vue'

export default {
  name: 'App',
  components: {
    Splash
  }
}
</script>

<style>
body {
  margin: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
  height: 100vh;
  width: 100vw;
  background-color: black;
  overflow: hidden;
}
</style>
