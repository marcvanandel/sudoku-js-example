<template>
  <div class="sudoku">
    <div class="row">
      <square squareRow=1 squareColumn=1></square>
      <square squareRow=1 squareColumn=2></square>
      <square squareRow=1 squareColumn=3></square>
    </div>
    <div class="row">
      <square squareRow=2 squareColumn=1></square>
      <square squareRow=2 squareColumn=2></square>
      <square squareRow=2 squareColumn=3></square>
    </div>
    <div class="row">
      <square squareRow=3 squareColumn=1></square>
      <square squareRow=3 squareColumn=2></square>
      <square squareRow=3 squareColumn=3></square>
    </div>
  </div>
</template>

<script>
import Square from './Square.vue'

export default {
  name: 'Sudoku',
  components: {
    Square
  },
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.sudoku {
  grid-template-columns: auto 300px 300px 300px auto;
  grid-template-rows: 300px 300px 300px;
}
</style>
