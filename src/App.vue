<template>
  <div id="app">
    <h1>Clicks per Date & Time Chart</h1>
    <Chart></Chart>
  </div>
</template>

<script>
import Chart from './components/clickChart.vue'

export default {
  name: 'app',
  components: {
    Chart
  }
}
</script>

<style>

body {
  background: #a19b9b;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  border-radius: 15px;
  box-shadow: 11px 6px 17px 17px rgba(25, 25, 25, 0.27);
  background-color: white;
  margin-top: 60px;
}

h1 {
  margin-top: 0;
  padding: 15px 0;
  color:  rgba(255, 0,0, 0.5);
  border-bottom: 1px solid #323d54;
}
</style>
