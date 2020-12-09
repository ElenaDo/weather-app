<template>
  <div id="app">
    <LocationSelector @citySelected="getWeather" />
  </div>
</template>

<script>
import LocationSelector from './components/LocationSelector.vue';

export default {
  name: 'App',
  components: {
    LocationSelector,
  },
  mounted() {
  },
  methods: {
    async getWeather({ city, country }) {
      try {
        const host = process.env.VUE_APP_HOST;
        const key = process.env.VUE_APP_KEY;
        console.log(host, key);
        const response = await fetch(`${host}/2.5/weather?q=${city},${country}&appid=${key}`);
        const result = await response.json();
        console.log(result);
      } catch (err) {
        console.log(err);
      }
    },
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
