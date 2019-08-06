<template>
  <div id="init">
    <div v-for="word in wordObjects" v-bind:key="word.id"> {{ word.word }} </div>
  </div>
</template>

<script>
export default {
  name: 'Words',
  props: ["wordObjects"]
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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
</style>