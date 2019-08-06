<template>
  <div class="wrapper">
    <div class="container">
      <div class="word" v-bind:style="{ fontFamily: fontFamily(), color: color(), fontSize: fontSize() + 'px' }" v-for="element in visibleWords" v-bind:key="element.key">{{ element }}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Words',
  props: ["visibleWords"],
  data() {
    return {
      fontFamilies: ["'Libre Caslon Text', serif", "'Roboto', sans-serif", "'Lobster', cursive", "'Barriecito', cursive", "'Neucha', cursive"],
      fontFamily: function (){
        return this.fontFamilies[Math.floor((Math.random() * this.fontFamilies.length))];
      },
      colors: ['gray', 'red', 'blue', 'magenta', 'orange', 'lightblue', 'white', 'lightgray'],
      color: function (){
        return this.colors[Math.floor((Math.random() * this.colors.length))];
      },
      fontSize: function (){
        return (Math.random() * 30) + 10;
      }
    }
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url('https://fonts.googleapis.com/css?family=Barriecito|Libre+Caslon+Text|Lobster|Neucha|Roboto&display=swap');
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.wrapper {
  padding-top: 10%;
  width: 80%;
}

.container {
  height: auto;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.word {
  display: inline-block;
  align-self: flex-end;
  padding-right: 1px;
  padding-left: 1px;
}
</style>