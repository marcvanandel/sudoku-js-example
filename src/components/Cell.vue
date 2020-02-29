<template>
  <div class="cell">[{{row}}, {{column}}]</div>
</template>

<script>
export default {
  name: "Cell",
  data: () => {
    return {
      number: 0,
    };
  },
  props: {
    x: Number
  },
  computed: {
    row: function() {
      return ((this.x - (this.x % 9)) / 9) + 1;
    },
    column: function() {
      return (this.x % 9) + 1;
    }
  }
};
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
