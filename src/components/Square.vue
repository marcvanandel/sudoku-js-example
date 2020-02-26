<template>
  <div class="square">
    <div class="row">
      <cell row={{ squareRow + 1 }} column={{ squareColumn + 1 }}></cell>
      <cell row={{ squareRow + 1 }} column={{ squareColumn + 2 }}></cell>
      <cell row={{ squareRow + 1 }} column={{ squareColumn + 3 }}></cell>
    </div>
    <div class="row">
      <cell row={{ squareRow + 2 }} column={{ squareColumn + 1 }}></cell>
      <cell row={{ squareRow + 2 }} column={{ squareColumn + 2 }}></cell>
      <cell row={{ squareRow + 2 }} column={{ squareColumn + 3 }}></cell>
    </div>
    <div class="row">
      <cell row={{ squareRow + 3 }} column={{ squareColumn + 1 }}></cell>
      <cell row={{ squareRow + 3 }} column={{ squareColumn + 2 }}></cell>
      <cell row={{ squareRow + 3 }} column={{ squareColumn + 3 }}></cell>
    </div>

  </div>
</template>

<script>
import Cell from './Cell.vue'

export default {
  name: 'Square',
  components: {
    Cell
  },
  props: {
    msg: String,
    squareRow: Number,
    squareColumn: Number
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.square {
  grid-template-columns: auto 100px 100px 100px auto;
  grid-template-rows: 100px 100px 100px;
}
</style>
