<template>
  <div id="app">
    <div class="menu">
      <ul>
        <span id="logo">Words</span>
        <li><vue-slider v-bind="sliderWords" v-model="amountOfWords" /></li>
        <li class="color-wrapper">FONT COLOR <verte picker="square" model="rgb" v-model="fontCol"></verte></li>
        <li>RANDOM FONT COLORS</li>
        <li>FONT FAMILY</li>
        <li class="color-wrapper">BACKGROUND COLOR<verte picker="square" model="rgb" v-model="backgroundCol"></verte></li>
        <li><button class="generate-button" v-on:click="spawnCheck">GENERATE</button></li>
      </ul>
    </div>
    <Words v-bind:visibleWords="visibleWords" :fontFam="fontFam" :fontCol="fontCol"/>
  </div>
</template>

<script>
import Words from './components/Words.vue'
import wordString from 'raw-loader!./wordlist.txt';

import VueSlider from 'vue-slider-component'
import 'vue-slider-component/theme/antd.css'

import Verte from 'verte';
import 'verte/dist/verte.css';

export default {
  name: 'app',
  components: {
    Words,
    VueSlider,
    Verte
  },
  data() {
    return {
      visibleWords: [],
      fontFam: "'Lobster', cursive",
      fontCol: '#FFF',
      backgroundCol: '',
      words: [],
      wordList: wordString.toUpperCase().split('\n'),
      spawned: false,

      // Slider for the amount of words, dont change amountOfWords!
      amountOfWords: 100,
      sliderWords: {
        min: 1,
        max: 200,
        height: 5,
        width: 240,
        dotSize: 20,
        tooltipPlacement: 'bottom',
        dotStyle: void 0,
        railStyle: void 0
      }
    }
  },
  methods: {
    // Checking if words are already there
    spawnCheck: function(){
      if(this.spawned == true){
        this.visibleWords = [];
        this.spawnWords();
      } else {
        this.spawnWords();
      }
    },
    // Spawn this.amountOfWords
    spawnWords: function(){
      this.wordList.forEach(element => {
        this.words.push(element);
      });
      for(let i = 0; i<this.amountOfWords; i++){
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

.color-wrapper {
  display: flex;
  justify-content: space-between;
  width: 15em;
  height: 20px;
}

.color {
  width: 22px;
  height: 22px;
  border-radius: 12px;
  border: 2px solid rgba(44, 195, 255, 0);
}

.color:hover {
  border: 2px solid rgba(0, 0, 0, 0.5);
}

.one {
  background: black;
}
.two {
  background: white;
}
.three {
  background: rgb(255, 60, 60);
}
.four {
  background: rgb(60, 60, 255);
}
.five {
  background: rgb(60, 255, 60);
}
.six {
  background: rgb(255, 60, 255);
}
</style>