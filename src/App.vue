<template>
  <div id="app">
    <h1>Learn Music with vue</h1>
    <div id="paper"></div>
    <textarea style="width: 100%" rows="10"></textarea>
  </div>
</template>

<script>
import abcjs from "abcjs";
export default {
  name: "App",
  components: {},
  mounted() {
    abcjs.renderAbc(
      "paper",
      `
    K:C
    DDAA|BBA2|
    `
    );
  }
};
</script>

<style lang="scss">
@import "codyhouse-framework/main/assets/css/base";

#app {
  font-family: "Open Sans", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
