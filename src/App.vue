<template>
  <div id="app">
    <div class="menu">
      <button v-on:click="spawnCheck">GENERATE</button>
      <span>AMOUNT OF WORDS</span>
      <span>COLOR</span>
      <span>FONT FAMILY</span>
      <span>BACKGROUND</span>
      <span>FONT SIZE</span>
      <span>SCREENSHOT</span>
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
      wordList: wordString.toUpperCase().split('\n'),
      spawned: false
    }
  },
  methods: {
    spawnCheck: function(){
      if(this.spawned == true){
        this.visibleWords = [];
        this.spawnWords();
      } else {
        this.spawnWords();
      }
    },
    spawnWords: function(){
      this.wordList.forEach(element => {
        this.words.push(element);
      });
      for(let i = 0; i<180; i++){
        let rand = Math.floor((Math.random() * 466551) + 1);
        this.visibleWords.push(this.words[rand]);
      }
      this.spawned = true;
    }
  }
}

</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Barriecito|Libre+Caslon+Text|Lobster|Neucha|Roboto&display=swap');
#app {
  font-family: 'Lobster', cursive;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #ffffff;
}
body {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  background: black;
}
.menu {
  display: flex;
  background:crimson;
  justify-content:space-evenly;
  align-items: center;
  height: 5vh;
}
</style>