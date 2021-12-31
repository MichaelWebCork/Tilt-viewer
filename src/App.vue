<template>
  <div id="app">
    <input type="file" @change="onSelectFile">
    <div ref="viewerRef"></div>
  </div>
</template>

<script>
import { Viewer as IcosaViewer } from 'icosa-viewer'

export default {
  name: 'App',
  components: {
  },
  data: function() {
    return {
      viewer: null,
    }
  },
  mounted() {
    this.viewer = new IcosaViewer(this.$refs.viewerRef)
  },
  methods: {
    onSelectFile(event) {
      const reader = new FileReader();
      reader.addEventListener("load", () => {
        console.log(reader.result)
        this.viewer.loadTiltGltf(reader.result)
      }, false);

      if (event.target.files[0]) {
        reader.readAsDataURL(event.target.files[0]);
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
