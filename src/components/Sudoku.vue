<template>
  <div class="sudoku">
    <cell v-for="x of Array(81).keys()" :key="x" v-bind:x="x">{{x}}</cell>
  </div>
</template>

<script>
import Cell from './Cell.vue'

export default {
  name: 'Sudoku',
  components: {
    Cell
  },
  props: {
    msg: String,
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.sudoku {
  display: inline-grid;
  grid-template-columns: auto auto auto auto auto auto auto auto auto;
  /* grid-template-rows: 55px 55px 55px 55px 55px 55px 55px 55px 55px; */
}
</style>
