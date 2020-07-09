<template>
  <transition
      @after-leave="fullyGone()"
      name="fade"
  >
    <div v-if="show" class="gallery">
      <div id="api-area">
        <h1 class="api-response-text" v-if="photos.length === 0">search for images</h1>
        <h1 class="api-response-text" v-if="photos.length !== 0">{{photos.length}} photos found</h1>
        <div id="api-controls">
          <div id="index-controls">
            <div @click="changeIndex('left')" id="left-arrow" class="nav-arrow"></div>
            <div @click="changeIndex('right')" id="right-arrow" class="nav-arrow"></div>
          </div>
          <h3>Controls</h3>
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
          <button @click="APICall()">CLICK</button>
        </div>
      </div>
      <div id="image-area">
        <div id="image-controls" v-if="photos[currentIndex] !== undefined">
          <!-- <img class="mars-photo" v-for="photo in photos" :key="photo.img_src" :src="photo.img_src"/> -->
          <ImageViewer :src="photos[currentIndex].img_src" />
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
import { bus } from '../main'
import ImageViewer from './ImageViewer'

export default {
  name: 'Gallery',
  components: {
    ImageViewer,
  },
  props: {
    msg: String
  },
  data() {
    return {
      sol: 1000,
      camera: 'any',
      rover: 'curiosity',
      photos: [],
      currentIndex: 0,
      show: false,
    }
  },
  mounted: function() {
    this.show = true;
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
      changeIndex: function(direction) {
          switch (direction) {
              case "left":
                  return this.currentIndex === 0 ? this.currentIndex = this.photos.length - 1 : this.currentIndex--;
              case "right":
                  return this.currentIndex === this.photos.length - 1 ? this.currentIndex = 0 : this.currentIndex++;
          }
      },
      fullyGone: function() {
        bus.$emit('gallery-fully-gone');
      },
      APICall: async function() {
          const url = `https://api.nasa.gov/mars-photos/api/v1/rovers/${this.rover}/photos?sol=${this.sol}${this.camera === "any" ? '' : `&camera=${this.camera}`}&api_key=${process.env.VUE_APP_API_KEY}`;
          const response = await fetch(url);
          const responseJSON = await response.json();
          this.currentIndex = 0;
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
.gallery {
  display: flex;
  justify-content: flex-start;
  align-items: center;
}
.api-response-text {
  position: absolute;
  top: 100px;
  left: 10px;
}
input, select, label, button {
  display: block;
  width: 100%;
}
#api-area {
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
#index-controls {
  width: 100%;
  display: flex;
  justify-content: space-around;
  align-items: center;
}
#api-controls {
  margin: 15px;
  width: 20vw;
  height: 30vh;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
}
#image-area {
  height: 100vh;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
#image-controls {
  display: flex;
  justify-content: space-around;
  align-items: center;
}
.nav-arrow {
  width: 20px;
  height: 20px;
  background-color: midnightblue;
}
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}
</style>
