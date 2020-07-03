<template>
    <div class="splash">
      <div class="content-wrapper">
        <img id="mars-img" alt="mars image" src="../assets/mars.png">
        <h1>
            MARS EXPLORER
        </h1>
        <p class="description">
            traverse the surface of Mars through images captured by Mars rovers
        </p>
        <button @click="enterSite()">enter</button>
        <img id="earth-img" alt="earth image" src="../assets/earth.png">
      </div>
    </div>
</template>

<script>
export default {
  name: 'Splash',
  components: {
    
  },
  props: {
    msg: String
  },
  methods: {
    enterSite: function() {
      this.$emit('enterSite');
    }
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
</style>
