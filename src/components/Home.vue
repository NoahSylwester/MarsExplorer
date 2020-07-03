<template>
    <div class="home">
        <h1>Home</h1>
        <button @click="APICall(1000)">CLICK</button>
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
      photos: []
    }
  },
  methods: {
      APICall: async function(sol) {
          const response = await fetch(`https://api.nasa.gov/mars-photos/api/v1/rovers/curiosity/photos?sol=${sol}&api_key=${process.env.VUE_APP_API_KEY}`);
          const responseJSON = await response.json();
          console.log(responseJSON);
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
