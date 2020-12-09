<template>
  <div id="app">
    <LocationSelector @citySelected="getByCity" @coordSelected="getByCoord" />
    <WeatherCard v-if="Object.keys(weatherData).length" :weatherData="weatherData"/>
  </div>
</template>

<script>
import LocationSelector from './components/LocationSelector.vue';
import WeatherCard from './components/WeatherCard.vue';

export default {
  name: 'App',
  data: () => ({
    weatherData: {},
  }),
  components: {
    LocationSelector,
    WeatherCard,
  },
  mounted() {
  },
  methods: {
    getByCity({ city, country }) {
      const query = `q=${city},${country}`;
      this.getWeather(query);
    },
    getByCoord({ lat, lon }) {
      const query = `lat=${lat}&lon=${lon}`;
      this.getWeather(query);
    },
    async getWeather(query) {
      try {
        const host = process.env.VUE_APP_HOST;
        const key = process.env.VUE_APP_KEY;
        console.log(host, key);
        const response = await fetch(`${host}/2.5/weather?${query}&units=metric&appid=${key}`);
        const result = await response.json();
        this.weatherData = result;
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
