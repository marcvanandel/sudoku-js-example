<template>
  <div id="sudoku">
    <div class="info">
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
    <div class="big-grid">
      <div v-for="s in squares" class="square" :key="s">
        <cell
          v-for="i in Array(3).keys()"
          :key="s+i"
          :ref="'cell-'+s+i"
          v-bind:data="data[s+i]"
          v-bind:selectedX="selected"
          v-on:sayHi="receiveMsg"
        >{{data[s]}}</cell>
        <cell
          v-for="i in Array(3).keys()"
          :key="s+i+9"
          :ref="'cell-'+s+i+9"
          v-bind:data="data[s+i+9]"
          v-bind:selectedX="selected"
          v-on:sayHi="receiveMsg"
        >{{data[s]}}</cell>
        <cell
          v-for="i in Array(3).keys()"
          :key="s+i+18"
          :ref="'cell-'+s+i+18"
          v-bind:data="data[s+i+18]"
          v-bind:selectedX="selected"
          v-on:sayHi="receiveMsg"
        >{{data[s]}}</cell>
      </div>
    </div>
  </div>
</template>

<script>
import Cell from "./Cell.vue";
import Data from "./Data.js";

export default {
  name: "Sudoku",
  components: {
    Cell
  },
  props: {},
  data: function() {
    var sqs = [0, 3, 6, 27, 30, 33, 54, 57, 60];
    var data = [];
    for (let x of Array(81).keys()) {
      data[x] = new Data(x, 0, false);
    }
    return {
      squares: sqs,
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
      if (!isNaN(c) && (!this.gameFixed || !this.data[this.selected].fixed)) {
        this.question = +c;
        this.data[this.selected].value = +c;
        this.data[this.selected].fixed = !this.gameFixed;
        // console.log(JSON.stringify(this.data[this.selected]));
      }
    },
    deleteValue: function() {
      if (!this.data[this.selected].fixed || !this.gameFixed) {
        this.data[this.selected].value = 0;
        this.data[this.selected].fixed = false;
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
      this.$refs["prepare"].checked = true;
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
.info {
  margin: 10px;
  display: block;
}
.grid {
  display: inline-grid;
  grid-template-columns: auto auto auto auto auto auto auto auto auto;
}
.big-grid {
  display: inline-grid;
  grid-template-columns: auto auto auto;
}
.big-grid div {
  border: 1px solid black;
}
.square {
  display: inline-grid;
  grid-template-columns: auto auto auto;
}
</style>
