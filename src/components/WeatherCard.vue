<template>
  <div class="main-container">
    <h2>Weather at</h2>
    <h4 v-if="weatherData.name">{{weatherData.name}}, {{getCountry(weatherData.sys.country)}} </h4>
    <h4 v-else>Coordinates {{weatherData.coord.lat}}, {{weatherData.coord.lon}}</h4>
    <p>Temperature {{weatherData.main.temp}} °C</p>
    <p>Feels like {{weatherData.main.feels_like}} °C</p>
    <p>Wind {{weatherData.wind.speed}} m/s</p>
  </div>
</template>

<script>
import { countries } from 'countries-list';

export default {
  name: 'WeatherCard',
  props: { weatherData: Object },
  methods: {
    getCountry(code) {
      return countries[code].name;
    },
  },
};
</script>
<style lang="scss" scoped>
.main-container {
  margin: auto;
  width: 50%;
  border-radius: .2em;
  border: 1px solid lightgrey;
  box-shadow: 3px 3px 3px lightgrey;
}
h4 {
  color: rgb(219, 76, 51);;
}
</style>
