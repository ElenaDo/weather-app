<template>
  <div>
    <input v-model="location.city" placeholder="City name">
    <select v-model="location.country">
      <option v-for="(country, key) of countries" :key="key" :value="key">
        {{country.name}}
      </option>
    </select>
    <button @click="request" :disabled="!location.city.length || !location.country">OK</button>
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
    request() {
      this.$emit('citySelected', this.location);
      console.log(this.location);
    },
  },
};
</script>
