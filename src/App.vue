<template>
  <div id="app" class="container padding-xxxs">
    <div class="text-center">
      <h1>Learn Music</h1>
    </div>
    <div id="paper"></div>
    <div class="abcjs-inline-midi"></div>
    <textarea
      spellcheck="false"
      v-model="note"
      class="note-input margin-top-lg padding-x-md"
      style="width: 100%"
      rows="10"
    ></textarea>
  </div>
</template>

<script>
import 'abcjs/abcjs-midi.css';
import abcjs from 'abcjs/midi';
export default {
  data() {
    return {
      note: `K:C
C D E F G A B c d e f g a b
`,
      opts: {
        viewportHorizontal: true,
        scrollHorizontal: true,
      },
    };
  },
  components: {},
  watch: {
    note(v) {
      abcjs.renderAbc('paper', this.note, this.opts);
    },
  },
  mounted() {
    abcjs.renderAbc('paper', this.note, this.opts);
  },
};
</script>

<style >
html,
body {
  font-size: 16px;
}
#app {
  font-family: 'Open Sans', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
.note-input {
  line-height: 1.65;
  caret-color: orange;
  background-color: #fff;
  background-image: linear-gradient(90deg, transparent 10px, #abced4 10px, #abced4 15px, transparent 15px),
    linear-gradient(#eee 0.1em, transparent 0.1em);
  background-size: 100% 1.675em;
}
</style>
