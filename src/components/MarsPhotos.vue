<template>
  <div class="search">
    <div class="hello">
      <h1>{{ msg }}</h1>
    </div>
    <button v-on:click="getResult()" class="search-button">Get Photos</button>
    <div class="results" v-if="results">
      <div v-for="result in results" v-bind:key="result.id">
        <img v-bind:src="result.img_src" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      // query: "",
      results: "",
    };
  },
  methods: {
    getResult() {
      axios
        .get(
          "https://api.nasa.gov/mars-photos/api/v1/rovers/curiosity/photos?sol=1000&page=1&api_key=DEMO_KEY"
        )
        .then((response) => {
          this.results = response.data.photos;
        });
    },
  },
  name: "MarsPhotos",
  props: {
    msg: String,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.results {
  margin-top: 10px;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 10px;
}
.results img {
  width: 31vw;
  height: auto;
  margin: 10px;
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
