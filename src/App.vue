<template>
  <div id="app">
    <Splash v-if="page === 'Splash'" @enterSite="changePage('Home')"/>
    <Home v-if="page === 'Home'" @returnToSplash="changePage('Splash')"/>
  </div>
</template>

<script>
import Splash from './components/Splash.vue'
import Home from './components/Home.vue'

export default {
  name: 'App',
  components: {
    Splash,
    Home
  },
  data() {
    return {
      page: "Splash"
    }
  },
  methods: {
    changePage: function(pageName) {
      this.page = pageName;
    }
  }
}
</script>

<style>
* {
  border: 0;
  margin: 0;
  padding: 0;
}
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
}
</style>
