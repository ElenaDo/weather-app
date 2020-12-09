<template>
  <div>
    <div class="selector-section">
      <select v-model="location.country">
        <option v-for="(country, key) of countries" :key="key" :value="key">
          {{country.name}}
        </option>
      </select>
      <input v-model="location.city" placeholder="City name">
      <button @click="request" :disabled="!location.city.length || !location.country">OK</button>
    </div>
    <button class="random-button" @click="genRandomCoord">Random location</button>
  </div>
</template>

<script>
import { countries } from 'countries-list';

export default {
  name: 'LocationSelector',
  data: () => ({
    city: '',
    location: {
      city: '',
      country: '',
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
      this.location.city = '';
      this.location.country = '';
    },
  },
};
</script>
<style lang="scss" scoped>
input, select{
  padding: .3em;
  margin: .2em;
  border: 1px solid lightgray;
  border-radius: .2em;
}
select {
  width: 150px;
}
button {
  padding: .4em .6em;
  border: 0px;
  border-radius: .2em;
  background-color: rgb(80, 172, 226);
  color: white;
  cursor: pointer;
  transition: background-color .5s;
  &:focus{
    outline: none;
  }
  &:hover{
    background-color: rgb(65, 195, 219);
  }
  &.random-button {
    margin: 1em 0 1em 0;
  }
  &:disabled{
    opacity: 0.5;
  }
}

.selector-section {
  display: flex;
  justify-content: center;
  align-items: center;
}
@media (max-width: 600px) {
  .selector-section {
    flex-direction: column;
    align-items: stretch;
  }
  select{
    width: 100%;
  }
  input, select, button {margin: 0.2em 0em}
  button {
    width: 100%;
  }
}
</style>
