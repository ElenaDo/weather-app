<template>
  <div>
    <input v-model="city" placeholder="City name">
    <button @click="request">OK</button>
  </div>
</template>

<script>
export default {
  name: 'LocationSelector',
  data: () => ({
    city: '',
  }),
  methods: {
    request() {
      this.$emit('citySelected', this.city);
    },
  },
};
</script>
