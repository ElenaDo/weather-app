<template>
  <div>
    <input v-model="location.city" placeholder="City name">
    <select v-model="location.country">
      <option v-for="(country, key) of countries" :key="key" :value="key">
        {{country.name}}
      </option>
    </select>
    <button @click="request" :disabled="!location.city.length || !location.country">OK</button>
    <div>
      <button @click="genRandomCoord">Randon location</button>
    </div>
  </div>
</template>

<script>
import { countries } from 'countries-list';

export default {
  name: 'LocationSelector',
  data: () => ({
    city: '',
    location: {
      city: 'Berlin',
      country: 'US',
    },
    countries,
  }),
  methods: {
    randomInterval(to, from) {
      return (Math.random() * (to - from) + from).toFixed(3) * 1;
    },
    genRandomCoord() {
      const lat = this.randomInterval(-90, 90);
      const lon = this.randomInterval(-180, 180);
      this.$emit('coordSelected', { lat, lon });
    },
    request() {
      this.$emit('citySelected', this.location);
      console.log(this.location);
    },
  },
};
</script>
