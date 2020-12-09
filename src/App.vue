<template>
  <div id="app">
  </div>
</template>

<script>

export default {
  name: 'App',
  components: {
  },
  mounted() {
    this.getWeather();
  },
  methods: {
    async getWeather() {
      try {
        const host = process.env.VUE_APP_HOST;
        const key = process.env.VUE_APP_KEY;
        console.log(host, key);
        const response = await fetch(`${host}=London&appid=${key}`);
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
