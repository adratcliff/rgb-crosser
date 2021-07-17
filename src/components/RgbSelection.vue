<template>
  <div class="rgb-selection">
    <span
      class="colour-indicator"
      :style="`background-color: rgb(${parseInt(red)}, ${parseInt(green)}, ${parseInt(blue)})`" />
    <button
      v-if="!hasChild"
      type="button"
      class="add-new"
      @click="hasChild = true">
      +
    </button>
    <div
      v-if="hasChild"
      class="colour-selection">
      <div class="colour-swap">
        <span
          class="colour-swap-label"
          :class="selection.red">
          {{ selection.red | capitalise }}
        </span>
        <button
          type="button"
          disabled>
          +
        </button>
        <button
          type="button"
          @click="swap('red', 'green')">
          -
        </button>
      </div>
      <div class="colour-swap">
        <span
          class="colour-swap-label"
          :class="selection.green">
          {{ selection.green | capitalise }}
        </span>
        <button
          type="button"
          @click="swap('green', 'red')">
          +
        </button>
        <button
          type="button"
          @click="swap('green', 'blue')">
          -
        </button>
      </div>
      <div class="colour-swap">
        <span
          class="colour-swap-label"
          :class="selection.blue">
          {{ selection.blue | capitalise }}
        </span>
        <button
          type="button"
          @click="swap('blue', 'green')">
          +
        </button>
        <button
          type="button"
          disabled>
          -
        </button>
      </div>
    </div>
    <rgb-selection
      v-if="hasChild"
      v-bind="colours" />
  </div>
</template>

<script>
export default {
  name: 'RgbSelection',
  props: {
    red: {
      type: String,
      default: '0',
    },
    green: {
      type: String,
      default: '0',
    },
    blue: {
      type: String,
      default: '0',
    },
  },
  data() {
    return {
      hasChild: false,
      selection: {
        red: 'red',
        green: 'green',
        blue: 'blue',
      }
    };
  },
  computed: {
    colours() {
      return {
        red: this[this.selection.red],
        green: this[this.selection.green],
        blue: this[this.selection.blue],
      };
    },
  },
  methods: {
    swap(a, b) {
      const tmp = this.selection[a];
      this.selection[a] = this.selection[b];
      this.selection[b] = tmp;
    },
  },
  filters: {
    capitalise(val) {
      return val.slice(0, 1).toUpperCase() + val.slice(1);
    },
  },
};
</script>

<style lang="scss" scoped>
.rgb-selection {
  display: flex;
  align-items: center;
  margin-left: 12px;
  .colour-indicator {
    height: 100px;
    width: 100px;
  }
  .colour-selection {
    margin-left: 16px;
    .colour-swap {
      display: flex;
      align-items: center;
      padding: 4px 0;
      .colour-swap-label {
        width: 50px;
        padding-right: 4px;
        text-align: right;
        display: inline-block;
        &.red { color: red; }
        &.green { color: lightgreen; }
        &.blue { color: lightblue; }
      }
    }
  }
  .add-new {
    height: 40px;
    width: 40px;
    margin: 0 12px;
    padding: 10px;
  }
}
</style>