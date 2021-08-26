<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" width="25%" />
    <h2>Hi ! <Typer ref="typer" title="This is my text" /></h2>
    <button @click="handleTyping">Type</button>
  </div>
</template>

<script>
import Typer from "./components/Typer";

export default {
  name: "App",
  components: {
    Typer,
  },
  methods: {
    handleTyping() {
      this.$refs.typer.typing();
    },
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
