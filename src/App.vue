<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <MarsPhotos msg="The Mars Files" />
  </div>
</template>

<script>
import MarsPhotos from "./components/MarsPhotos.vue";

export default {
  name: "App",
  components: {
    MarsPhotos,
  },
};
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
