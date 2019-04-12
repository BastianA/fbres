<template>
  <div id="app">
    <Chart title="Data visualization"/>
  </div>
</template>

<script>
window.csvToArray = require('csv-to-array');
import Chart from './components/Chart.vue'

export default {
  name: 'fbres',
  components: {
    Chart
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
