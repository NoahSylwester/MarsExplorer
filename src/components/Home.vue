<template>
    <div class="home">
        <h1>Home</h1>
        <button @click="APICall()">CLICK</button>
        <label for="sol-input">Sol</label>
        <input id="sol-input" name="sol-input" type="number" placeholder="1000" @change="changeSol($event.target.value)" />
        <label for="camera-input">Camera</label>
        <select id="camera-input" name="camera-input" @change="changeCamera($event.target.value)">
          <option value="FHAZ">FHAZ</option>
          <option value="RHAZ">RHAZ</option>
          <option value="MAST">MAST</option>
          <option value="CHEMCAM">CHEMCAM</option>
          <option value="MAHLI">MAHLI</option>
          <option value="MARDI">MARDI</option>
          <option value="NAVCAM">NAVCAM</option>
          <option value="PANCAM">PANCAM</option>
          <option value="MINITES">MINITES</option>
        </select>
        <label for="rover-input">Rover</label>
        <select id="rover-input" name="rover-input" @change="changeRover($event.target.value)">
          <option value="Curiosity">Curiosity</option>
          <option value="Opportunity">Opportunity</option>
          <option value="Spirit">Spirit</option>
        </select>
        <img class="mars-photo" v-for="photo in photos" :key="photo.img_src" :src="photo.img_src"/>
    </div>
</template>

<script>
export default {
  name: 'Home',
  props: {
    msg: String
  },
  data() {
    return {
      sol: 1,
      camera: '',
      rover: '',
      photos: []
    }
  },
  methods: {
      changeSol: function(newSol) {
        this.sol = newSol;
      },
      changeCamera: function(newCamera) {
        this.camera = newCamera;
      },
      changeRover: function(newRover) {
        this.rover = newRover;
      },
      APICall: async function() {
          const response = await fetch(`https://api.nasa.gov/mars-photos/api/v1/rovers/curiosity/photos?sol=${this.sol}&api_key=${process.env.VUE_APP_API_KEY}`);
          const responseJSON = await response.json();
          this.photos = responseJSON.photos.slice(0,5);
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.mars-photo {
  width: 200px;
  height: 200px;
  object-fit: cover;
}
</style>
