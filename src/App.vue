<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" width="15%" />
    <h2 style="display: flex; flex-direction: column">
      Hi !
      <Typer
        ref="typer"
        :phrases="[
          'I love to create things with Vue',
          'Also with React',
          'And sometimes with Svelte...',
          'Yes... I hate Angular.'
        ]"
        :text-styles="{color: '#000'}"
        cursor-default-color="orange"
        cursor-active-color="red"
        cursor-width="3px"
      />
    </h2>
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
