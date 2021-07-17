<template>
  <div id="app">
    <div class="initial-selectors">
      <label for="red-input">
        Red
      </label>
      <input
        v-model="red"
        id="red-input"
        type="number"
        min="0"
        max="255"
        step="1">
      <label for="green-input">
        Green
      </label>
      <input
        v-model="green"
        id="green-input"
        type="number"
        min="0"
        max="255"
        step="1">
      <label for="red-input">
        Blue
      </label>
      <input
        v-model="blue"
        id="blue-input"
        type="number"
        min="0"
        max="255"
        step="1">
    </div>
    <rgb-selection
      :red="red"
      :green="green"
      :blue="blue" />
  </div>
</template>

<script>
import RgbSelection from './components/RgbSelection';

export default {
  name: 'App',
  components: {
    RgbSelection,
  },
  data() {
    return {
      red: '0',
      green: '0',
      blue: '0',
    };
  },
};
</script>

<style lang="scss">
html {
  background-color: #2c3e50;
  color: #fafafa;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  display: flex;
  flex-direction: row;
  align-items: center;
  height: 100vh;
  .initial-selectors {
    display: flex;
    flex-direction: column;
    justify-content: center;
    text-align: left;
    label {
      padding: 4px 0;
    }
  }
}
</style>
