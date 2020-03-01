<template>
  <div class="cell" v-on:click="emitCoords" v-bind:class="[{ selected: isSelected}, {clFixed: isFixed }]">{{ (data.value != 0) ? data.value : ''}}</div>
</template>

<script>
import Data from "./Data.js";

export default {
  name: "Cell",
  data: () => {
    return {
      number: 0
    };
  },
  props: {
    data: Data,
    selectedX: Number,
  },
  computed: {
    row: function() {
      return ((this.data.id - (this.data.id % 9)) / 9) + 1;
    },
    column: function() {
      return (this.data.id % 9) + 1;
    },
    isSelected: function() {
      return this.selectedX == this.data.id;
    },
    isFixed: function() {
      return this.data.fixed;
    }
  },
  methods: {
    emitCoords: function() {
      this.$emit('sayHi', this.data.id)
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.cell {
  /* display: inline-block; */
  border: 1px solid black;
  width: 50px;
  height: 50px;
  text-align: center;
  line-height: 50px;
  font-size: 2em;
  color: blue;
}
.selected {
  background-color: yellow;
}
.clFixed {
  font-weight: bold;
  color: black;
}
</style>
