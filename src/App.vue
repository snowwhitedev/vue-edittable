<template>
  <div id="app">
    <SampleData />
  </div>
</template>

<script>
import SampleData from './views/SampleData.vue'

export default {
  name: 'App',
  components: {
    SampleData
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
