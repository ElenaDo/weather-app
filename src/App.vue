<template>
  <div id="app">
    <LocationSelector @citySelected="getByCity" @coordSelected="getByCoord" />
    <WeatherCard v-if="Object.keys(weatherData).length" :weatherData="weatherData"/>
    <p v-else>Please choose location</p>
    <p v-if="errorMessage" class="error">{{errorMessage}}</p>
  </div>
</template>

<script>
import LocationSelector from './components/LocationSelector.vue';
import WeatherCard from './components/WeatherCard.vue';

export default {
  name: 'App',
  data: () => ({
    weatherData: {},
    errorMessage: '',
    responseCache: {},
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
      this.errorMessage = '';
      if (this.responseCache[query]) {
        this.weatherData = this.responseCache[query];
        return;
      }
      try {
        this.weatherData = {};
        const host = process.env.VUE_APP_HOST;
        const key = process.env.VUE_APP_KEY;
        const response = await fetch(`${host}/2.5/weather?${query}&units=metric&appid=${key}`);
        if (!response.ok) {
          if (response.status === 404) {
            this.errorMessage = 'City not found';
          } else {
            this.errorMessage = response.statusText;
          }
          return;
        }
        const result = await response.json();
        this.responseCache[query] = result;
        this.weatherData = result;
      } catch (err) {
        // eslint-disable-next-line no-console
        console.error(err);
        this.errorMessage = 'Connection error';
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
  padding: 1em;
}
.error {
  color: red
}
</style>
