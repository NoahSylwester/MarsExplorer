<template>
  <transition
      name="fade"
    >
    <div v-if="show" class="image-viewer">
        <img :src="src" class="viewed-image" />
    </div>
  </transition>
</template>

<script>
// import { bus } from '../main'

export default {
  name: 'ImageViewer',
  props: {
    src: String,
  },
  data() {
    return {
      show: false,
    }
  },
  mounted: function() {
    this.show = true;
  },
  methods: {
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.viewed-image {
  border: 2px midnightblue solid;
  box-shadow: 0 0 1000px 0px midnightblue;
  width: 60vw;
  height: 60vw;
  object-fit: cover;
  -webkit-touch-callout: none; /* iOS Safari */
  -webkit-user-select: none; /* Safari */
  -khtml-user-select: none; /* Konqueror HTML */
  -moz-user-select: none; /* Old versions of Firefox */
  -ms-user-select: none; /* Internet Explorer/Edge */
  user-select: none;
}
.fade-enter-active, .fade-leave-active {
  transition: opacity 1s;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}
</style>
