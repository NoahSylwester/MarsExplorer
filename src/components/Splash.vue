<template>
  <transition
    @after-enter="showButton = true"
    @after-leave="fullyGone()"
    name="fade"
  >
      <div v-if="show" class="splash">
        <div class="content-wrapper">
          <img id="mars-img" alt="mars image" src="../assets/mars.png">
          <h1>
              MARS EXPLORER
          </h1>
          <p class="description">
              traverse the surface of Mars through images captured by Mars rovers
          </p>
          <transition name="fadeButton">
            <button v-if="showButton" @click="enterSite()">enter</button>
          </transition>
          <div v-if="!showButton" class="buttonSubstitute"></div>
          <img id="earth-img" alt="earth image" src="../assets/earth.png">
        </div>
      </div>
  </transition>
</template>

<script>
import { bus } from '../main'

export default {
  name: 'Splash',
  data() {
    return {
      show: false,
      showButton: false
    }
  },
  components: {
    
  },
  props: {
    msg: String
  },
  mounted: function() {
    this.show = true;
  },
  methods: {
    enterSite: function() {
      this.$emit('enter-site');
    },
    fullyGone: function() {
      bus.$emit('splash-fully-gone');
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#mars-img {
  width: 10vw;
  height: 10vw;
  object-fit: cover;
}
#earth-img {
  width: 60vw;
  height: 60vw;
  object-fit: cover;
  border-radius: 1000vw;
}
.splash {
    height: 100vh;

    overflow: hidden;
}
.content-wrapper {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}
.description {
  margin: 20px;
}
.buttonSubstitute {
    width: 7vw;
    height: 7vw;
    border: 0;
}
button {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    background-color: black;
    color: white;
    border: 0;
    font-size: 2vw;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 7vw;
    height: 7vw;
    padding: 10px;
    border-radius: 100px;
    box-shadow: 0 0 40px white;
    transition: 0.2s;
    cursor: pointer;
}
button:hover {
    background-color: white;
    color: black;
}
button:focus {
    outline: none;
}
.fade-enter-active {
  transition: opacity 2s;
}
.fade-leave-active {
  transition: opacity 1s;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}
.fadeButton-enter-active, .fadeButton-leave-active {
  transition: opacity 1.5s ease-in;
}
.fadeButton-enter, .fadeButton-leave-to {
  opacity: 0;
}
</style>
