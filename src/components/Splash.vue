<template>
    <div class="splash">
        <img id="mars-img" alt="mars image" src="../assets/mars.png">
        <h1>
            MARS EXPLORER
        </h1>
        <p>
            traverse the surface of Mars through images captured by Mars rovers
        </p>
        <button @click="enterSite()">enter</button>
        <img id="earth-img" alt="earth image" src="../assets/earth.png">
    </div>
</template>

<script>
export default {
  name: 'Splash',
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
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
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
    padding: 30px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
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
