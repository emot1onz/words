<template>
  <div id="app">
    <Words v-bind:wordObjects="wordObjects" />
    <button v-on:click="readFile">Click me</button>
  </div>
</template>

<script>
import Words from './components/Words.vue'
import wordString from 'raw-loader!./wordlist.txt';

export default {
  name: 'app',
  components: {
    Words
  },
  data() {
    return {
      wordObjects: [],
      wordList: wordString.split('\n')
    }
  },
  methods: {
    readFile: function(){
      this.wordList.forEach(function(element, key) {
        this.wordObjects.push({id: key, word: element});
      });
    },
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
