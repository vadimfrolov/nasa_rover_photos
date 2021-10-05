<template>
  <div>
    <div class="hello">
      <h1>{{ msg }}</h1>
    </div>
    <button v-on:click="getResult()" class="search-button">Get Photos</button>
    <section v-if="errored">
      <p>
        Something is wrong 😞 <br />
        We are sorry
      </p>
    </section>
    <section v-else>
      <div v-if="loading" class="lds-hourglass" />
      <div v-else>
        <div class="wrapper">
          <aside v-if="results" class="sidebar">
            <select
              name="rovers"
              id="rover-select"
              @change="switchSelect($event)"
            >
              <option
                v-for="option in options"
                v-bind:value="option.value"
                v-bind:key="option.id"
              >
                {{ option.text }}
              </option>
            </select>
          </aside>
          <div class="results" v-if="results">
            <div v-for="result in results" v-bind:key="result.id">
              <img v-bind:src="result.img_src" />
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      query: "curiosity",
      results: null,
      loading: false,
      errored: false,
      options: [
        { id: 1, text: "Curiosity", value: "curiosity" },
        { id: 2, text: "Opportunity", value: "opportunity" },
        { id: 3, text: "Spirit", value: "spirit" },
      ],
    };
  },
  methods: {
    getResult() {
      let pageCounter = 1;
      window.onscroll = () => {
        let bottomOfWindow =
          document.documentElement.scrollTop + window.innerHeight ===
          document.documentElement.offsetHeight;
        if (bottomOfWindow) {
          pageCounter += 1;
          axios
            .get(
              `https://api.nasa.gov/mars-photos/api/v1/rovers/${this.query}/photos?sol=1000&page=${pageCounter}&api_key=NBotRn43dEjGTMX6aiFUOpajms3zNR0Vejec6sOl`
            )
            .then((response) => {
              this.results.push(...response.data.photos);
            });
        }
      };
      this.loading = true;
      axios
        .get(
          `https://api.nasa.gov/mars-photos/api/v1/rovers/${this.query}/photos?sol=1000&page=1&api_key=NBotRn43dEjGTMX6aiFUOpajms3zNR0Vejec6sOl`
        )
        .then((response) => {
          this.results = response.data.photos;
        })
        .catch((error) => {
          console.log(error);
          this.errored = true;
        })
        .finally(() => (this.loading = false));
    },
    switchSelect(event) {
      this.query = event.target.value;
      axios
        .get(
          `https://api.nasa.gov/mars-photos/api/v1/rovers/${this.query}/photos?sol=1000&page=1&api_key=NBotRn43dEjGTMX6aiFUOpajms3zNR0Vejec6sOl`
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
.wrapper {
  display: flex;
}
.results {
  width: 72vw;
  margin-top: 10px;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 10px;
  justify-self: center;
}
.results img {
  width: 23vw;
  height: auto;
  margin: 10px;
}

.sidebar {
  background-color: #105bd8;
  width: 25vw;
  height: auto;
}

select {
  width: 10vw;
  padding: 5px;
  margin-top: 10px;
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

.lds-hourglass {
  display: inline-block;
  position: relative;
  width: 80px;
  height: 80px;
}
.lds-hourglass:after {
  content: " ";
  display: block;
  border-radius: 50%;
  width: 0;
  height: 0;
  margin: 8px;
  box-sizing: border-box;
  border: 32px solid #105bd8;
  border-color: #105bd8 transparent #105bd8 transparent;
  animation: lds-hourglass 1.2s infinite;
}
@keyframes lds-hourglass {
  0% {
    transform: rotate(0);
    animation-timing-function: cubic-bezier(0.55, 0.055, 0.675, 0.19);
  }
  50% {
    transform: rotate(900deg);
    animation-timing-function: cubic-bezier(0.215, 0.61, 0.355, 1);
  }
  100% {
    transform: rotate(1800deg);
  }
}
</style>
