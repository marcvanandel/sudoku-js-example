<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/sudoku-example.png" width="200px">
    <h2>Sudoku</h2>
    <sudoku />
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import Sudoku from './components/Sudoku.vue'

export default {
  name: 'App',
  components: {
    Sudoku
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
