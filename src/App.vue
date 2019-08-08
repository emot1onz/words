<template>
  <div id="app">
    <div class="menu">
      <ul><li class="logo-padding"><span id="logo" v-on:click="toggleMenu()">Words</span></li></ul>
      <ul v-if="menuOpen">
        <li><vue-slider v-bind="sliderWords" v-model="amountOfWords" /></li>
        <li class="wrapper">FONT COLOR <verte picker="square" model="rgb" v-model="fontCol"></verte></li>
        <li class="wrapper">RANDOM FONT COLORS
          <button v-on:click='toggleRandomFontColors()'> {{ randomFontColors }} </button> 
        </li>
        <li>
          <dropdown :x="-10">
            <template slot="btn">FONT FAMILY</template>
            <template slot="body">
                <li class="list" v-for="font in fontFamilies" v-bind:key="font.name">
                  <button class="list-btn" v-on:click="fontFam = font.name">
                    {{font.name}}
                  </button>  
                </li>
            </template>
          </dropdown>
        </li>
        <li class="wrapper">BACKGROUND COLOR<verte picker="square" model="rgb" v-model="backgroundCol"></verte></li>
        <li>SCREENSHOT</li>
        <li><button class="generate-button" v-on:click="spawnCheck" :click="setBackgroundColors()">GENERATE</button></li>
      </ul>
      <p class="menu-closer" v-if="menuOpen" v-on:click="toggleMenu()">^</p>
    </div>
    <Words v-bind:visibleWords="visibleWords" :fontFam="fontFam" :fontCol="fontCol" :randomFontColors="randomFontColors"/>
  </div>
</template>

<script>
import Words from './components/Words.vue';
import wordString from 'raw-loader!./wordlist.txt';

import VueSlider from 'vue-slider-component';
import 'vue-slider-component/theme/antd.css';

import Verte from 'verte';
import 'verte/dist/verte.css';

import Dropdown from 'bp-vuejs-dropdown';

export default {
  beforeCreate: function() {
        document.body.className = 'home';
  },
  name: 'app',
  components: {
    Words,
    VueSlider,
    Verte,
    Dropdown
  },
  data() {
    return {
      visibleWords: [],
      fontFam: 'RANDOM',
      fontCol: '#ce2121',
      backgroundCol: '#000',
      words: [],
      wordList: wordString.toUpperCase().split('\n'),
      spawned: false,
      randomFontColors: true,
      menuOpen: true,
      fontFamilies: [
        {id: 1, active: true, name: "RANDOM"},
        {id: 2, active: false, name: "'Libre Caslon Text', serif"}, 
        {id: 3, active: false, name: "'Roboto', sans-serif"}, 
        {id: 4, active: false, name: "'Lobster', cursive"},
        {id: 5, active: false, name: "'Barriecito', cursive"},
        {id: 6, active: false, name: "'Neucha', cursive"}],

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
    },
    toggleRandomFontColors: function (){
      this.randomFontColors = !this.randomFontColors;
    },
    toggleMenu: function (){
      this.menuOpen = !this.menuOpen;
    },
    setBackgroundColors: function(){
        let body = document.querySelector('.home');
        body.setAttribute('style', 'background:' + this.backgroundCol + ';');
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
}
.menu {
  position: absolute;
  width: 20em;
  background: rgba(255, 255, 255, 90%);
  height: auto;
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
  padding: 5px;
  font-size: 1.2em;
  box-shadow: -4px 4px 2px 1px rgba(0, 0, 0, .2);
}

.wrapper {
  display: flex;
  justify-content: space-between;
  width: 15em;
  height: 20px;
}

.list {
  padding: 3px 3px 2px 5px;
}

.list:hover {
  background: lightgray;
}

.list-btn {
  border: none;
  background: rgba(255, 255, 255, 0%);
}

.menu-closer {
  font-size: 2em;
  font-weight: 500;
  text-align: center;
  margin: 0;
  cursor: pointer;
}

.logo-padding {
  padding: 0;
  cursor: pointer;
}
</style>