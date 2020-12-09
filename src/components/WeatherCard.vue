<template>
  <div class="main-container">
    <h2>Weather at</h2>
    <h4 v-if="weatherData.name">{{weatherData.name}}, {{weatherData.sys.country}} </h4>
    <h4 v-else>Coordinates {{weatherData.coord.lat}}, {{weatherData.coord.lon}}</h4>
    <p>Temperature {{weatherData.main.temp}} °C</p>
    <p>Feels like {{weatherData.main.feels_like}} °C</p>
    <p>Wind {{weatherData.wind.speed}} m/s</p>
  </div>
</template>

<script>
export default {
  name: 'WeatherCard',
  props: { weatherData: Object },
};
</script>
<style lang="scss" scoped>
</style>
