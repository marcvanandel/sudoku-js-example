<template>
  <div class="cell">
    [{{row}}, {{column}}]
  </div>
</template>

<script>
export default {
  name: 'Cell',
  props: {
    number: Number,
    row: Number,
    column: Number
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.cell {
  display: inline-block;
  border: 1px solid black;
  width: 50px;
  height: 50px;
  text-align: center;
  line-height: 50px;
}
</style>
