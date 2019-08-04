<template>
  <div id="app">
    <Words />
  </div>
</template>

<script>
import Words from './components/Words.vue'

export default {
  name: 'app',
  components: {
    Words
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
