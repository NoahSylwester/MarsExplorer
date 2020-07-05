<template>
    <div class="home">
        <h1>Home</h1>
        <button @click="APICall()">CLICK</button>
        <label for="sol-input">Sol</label>
        <input id="sol-input" name="sol-input" type="number" :value="sol" @change="changeSol($event.target.value)" />
        <label for="camera-input">Camera</label>
        <select id="camera-input" :value="camera" name="camera-input" @change="changeCamera($event.target.value)">
          <option value="any">Any</option>
          <option value="fhaz">FHAZ</option>
          <option value="rhaz">RHAZ</option>
          <option value="mast">MAST</option>
          <option value="chemcam">CHEMCAM</option>
          <option value="mahli">MAHLI</option>
          <option value="mardi">MARDI</option>
          <option value="navcam">NAVCAM</option>
          <option value="pancam">PANCAM</option>
          <option value="minites">MINITES</option>
        </select>
        <label for="rover-input">Rover</label>
        <select id="rover-input" name="rover-input" @change="changeRover($event.target.value)">
          <option value="curiosity">Curiosity</option>
          <option value="opportunity">Opportunity</option>
          <option value="spirit">Spirit</option>
        </select>
        <div>
          <img class="mars-photo" v-for="photo in photos" :key="photo.img_src" :src="photo.img_src"/>
        </div>
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
      sol: 1000,
      camera: 'any',
      rover: 'curiosity',
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
          const url = `https://api.nasa.gov/mars-photos/api/v1/rovers/${this.rover}/photos?sol=${this.sol}${this.camera === "any" ? '' : `&camera=${this.camera}`}&api_key=${process.env.VUE_APP_API_KEY}`;
          const response = await fetch(url);
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
