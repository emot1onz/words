<template>
  <div id="app">
    <div class="menu">
      <ul>
        <span id="logo">Words</span>
        <li>AMOUNT OF WORDS</li>
        <li>COLOR</li>
        <li>FONT FAMILY</li>
        <li>BACKGROUND</li>
        <li>FONT SIZE</li>
        <li><button class="generate-button" v-on:click="spawnCheck">GENERATE</button></li>
      </ul>
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
      for(let i = 0; i<100; i++){
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
  display: flex;
  justify-content: center;
  font-family: 'Roboto', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: black;
}
body {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  background: black;
}
.menu {
  position: absolute;
  transform: translateX(-20em);
  width: 20em;
  background: rgba(255, 255, 255, 80%);
  height: 100vh;
}
ul {
  list-style: none;
  height: 100%;
}
li {
  padding: 2em 0;
}
#logo {
  font-family: 'Lobster', cursive;
  font-size: 2em;
  margin-bottom: 20px;
}
.generate-button {
  background: #ffffff;
  border: 1px solid #ffffff;
  border-radius: 15px;
  font-size: 1.2em;
}
</style>