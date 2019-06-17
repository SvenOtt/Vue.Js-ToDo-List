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
body {
  background-color: hotpink
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 140px;
  font-size: 50px;
}
</style>
