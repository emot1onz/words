<template>
  <div id="app">
    <div class="menu">
      <button v-on:click="readFile">Read the File</button>
      <button v-on:click="chooseWords">Spawn 1000 Words</button>
    </div>
    <Words v-bind:visibleWords="visibleWords" />
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
      visibleWords: [],
      words: [],
      wordList: wordString.toUpperCase().split('\n')
    }
  },
  methods: {
    readFile: function(){
      this.wordList.forEach(element => {
        this.words.push(element);
      });
    },
    chooseWords: function(){
      for(let i = 0; i<1000; i++){
        let rand = Math.floor((Math.random() * 466551) + 1);
        this.visibleWords.push(this.words[rand]);
      }
    }
  }
}

</script>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
body {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
.menu {
  display: flex;
  justify-content: center;
}
</style>