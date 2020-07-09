<template>
  <div id="app">
    <Splash
      v-if="page === 'Splash'"
      @enter-site="changePage('')"
    />
    <Gallery
      v-if="page === 'Gallery'" 
      @return-to-splash="changePage('Splash')"
    />
  </div>
</template>

<script>
import Splash from './components/Splash.vue'
import Gallery from './components/Gallery.vue'
import { bus } from './main'

export default {
  name: 'App',
  components: {
    Splash,
    Gallery
  },
  data() {
    return {
      page: "Splash"
    }
  },
  created (){
    bus.$on('splash-fully-gone', () => {
      this.changePage('Gallery');
    })
  },
  methods: {
    changePage: function(pageName) {
      this.page = pageName;
    },
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
  height: auto;
  min-height: 100vh;
  width: 100vw;
  background-color: black;
  overflow: contain;
}
</style>
