<template>
  <div id="sudoku">
    <div>
      <p>{{ msg }}</p>
      <button id="reset" v-on:click="reset">Reset</button>
      <input
        type="radio"
        id="prepare"
        ref="prepare"
        name="gameMode"
        value="prepare"
        checked
        v-on:click="toggleFixed"
      />
      <label for="prepare">Instellen</label>
      <input type="radio" id="play" name="gameMode" value="play" v-on:click="toggleFixed" />
      <label for="play">Spelen</label>
    </div>
    <div class="grid">
      <cell
        v-for="x in data"
        :key="x.id"
        :ref="'cell-'+x.id"
        v-bind:x="x.id"
        v-bind:value="x.value"
        v-bind:fixed="x.fixed"
        v-bind:selectedX="selected"
        v-on:sayHi="receiveMsg"
      >{{x}}</cell>
    </div>
  </div>
</template>

<script>
import Cell from "./Cell.vue";

export default {
  name: "Sudoku",
  components: {
    Cell
  },
  props: {},
  data: function() {
    var data = [];
    for (let x of Array(81).keys()) {
      data[x] = { id: x, value: 0, fixed: false };
    }
    return {
      data: data,
      selected: 0,
      gameFixed: false,
      question: ""
    };
  },
  computed: {
    msg: function() {
      return "selected: " + this.selected + "; " + this.question;
    }
  },
  methods: {
    receiveMsg(x) {
      this.selected = x;
    },
    calcSelected: function(x) {
      return x == this.selected;
    },
    handleInput: function(c) {
      if (!isNaN(c)) {
        this.question = +c;
        this.data[this.selected].value = +c;
        this.data[this.selected].fixed = !this.gameFixed;
        console.log(JSON.stringify(this.data[this.selected]));
      }
    },
    deleteValue: function() {
      if (!this.data[this.selected].fixed || !this.gameFixed) {
        this.data[this.selected].value = 0;
      }
    },
    up: function() {
      if (this.selected >= 9) this.selected = this.selected - 9;
    },
    down: function() {
      if (this.selected < 81 - 9) this.selected = this.selected + 9;
    },
    left: function() {
      if (this.selected % 9 > 0) this.selected = this.selected - 1;
    },
    right: function() {
      if (this.selected % 9 < 8) this.selected = this.selected + 1;
    },
    reset: function() {
      for (let index = 0; index < this.data.length; index++) {
        this.data[index].value = 0;
      }
      this.selected = 0;
      this.gameFixed = false;
      this.$refs['prepare'].checked = true;
      document.activeElement.blur();
    },
    toggleFixed: function() {
      this.gameFixed = !this.gameFixed;
      document.activeElement.blur();
    }
  },
  mounted: function() {
    window.addEventListener("keyup", event => {
      switch (event.keyCode) {
        case 37:
          this.left();
          break;
        case 39:
          this.right();
          break;
        case 38:
          this.up();
          break;
        case 40:
          this.down();
          break;
        case 8:
        case 46:
          this.deleteValue();
          break;
        default:
          this.handleInput(event.key);
          break;
      }
    });
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.grid {
  display: inline-grid;
  grid-template-columns: auto auto auto auto auto auto auto auto auto;
}
</style>
