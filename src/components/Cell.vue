<template>
  <div class="cell" v-on:click="emitCoords" v-bind:class="[{ selected: isSelected}, {clFixed: isFixed }]">{{ (value != 0) ? value : ''}}</div>
</template>

<script>
export default {
  name: "Cell",
  data: () => {
    return {
      number: 0
    };
  },
  props: {
    x: Number,
    selectedX: Number,
    value: Number,
    fixed: Boolean
  },
  computed: {
    row: function() {
      return ((this.x - (this.x % 9)) / 9) + 1;
    },
    column: function() {
      return (this.x % 9) + 1;
    },
    isSelected: function() {
      return this.selectedX == this.x;
    },
    isFixed: function() {
      return this.fixed;
    }
  },
  methods: {
    emitCoords: function() {
      this.$emit('sayHi', this.x)
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
