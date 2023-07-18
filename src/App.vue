<template>
  <the-weather></the-weather>
</template>

<script>
import TheWeather from './components/TheWeather.vue'

export default {
  name: 'App',
  components: {
    TheWeather
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
