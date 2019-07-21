<template>
  <div id="app">
    
    <ToDo />
  </div> 
</template>

<script>
import ToDo from './components/ToDo.vue'

export default {
  name: "app",
  components: {
    ToDo
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Montserrat:400,700');

body {
  background: linear-gradient(black, #000099, #66c2ff, #ffcccc, #ffeee6);;
  font-family: 'Montserrat', sans-serif;
  display: grid;
  grid-template-rows: auto;
  justify-items: center;
  align-items: center;
}
body, html {
  margin: 0;
  height: 100%;
}
#app {
    width: 50%;
}
</style>
