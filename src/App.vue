<template>
  <div id="app">
    <h1>Footylights</h1>
    <Highlights/>
  </div>
</template>

<script>
import Highlights from './components/Highlights.vue'

export default {
  name: 'App',
  components: {
    Highlights
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
  margin-top: 40px;
}
</style>
