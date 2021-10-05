<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <MarsPhotos msg="The Mars Files" />
    <button class="search-button">Get Photos</button>
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

.search-button {
  background-color: #105bd8;
  border-radius: 5px;
  border-width: 0;
  color: #fff;
  cursor: pointer;
  font-size: 1.7rem;
  display: inline-block;
  font-weight: 700;
  line-height: 1.5;
  padding: 1rem 2rem;
  text-align: center;
  text-decoration: none;
  vertical-align: baseline;
  white-space: nowrap;
  touch-action: manipulation;
}
</style>
