<template>
  <div id="app" class="container padding-xxxs">
    <div class="text-center margin-bottom-sm">
      <h1>Learn Music</h1>
    </div>
    <div id="main-midi"></div>
    <textarea
      spellcheck="false"
      v-model="note"
      class="note-input margin-top-sm padding-x-md"
      style="width: 100%"
      rows="10"
    ></textarea>
    <div>
      <div id="paper"></div>
    </div>
  </div>
</template>

<script>
import abcjs from 'abcjs';
export default {
  data() {
    return {
      control: null,
      note: `%%MIDI program 0
X:1
T:"Silent Night"
C:Franz Xaver Gruber
Q:160
K:C
M:4/4
f3gf2 d6 | f3gf2 d6 | c'4c'2 a6 | _b4_b2 f6 | 
g4g2 _b3ag2 | f3gf2 d6| g4g2 _b3ag2| f3gf2 d6| 
c'4c'2 _e'3c'a2 | _b6 d'6 | _b2f2d2 f3_ec2_ | _B6 z6|
d3_ed2 _B6 | d3_ed2 _B6 | _e4 _e2 _e6 | d4_e2 d6|
_e4_e2 g3f_e2 | d3_ed2 _B6 | _e4_e2 g3f_e2 | d3_ed2 _B6 |
_e4_e2 c3_ec2 | d6 f6 | d4 _B2 A3AA2 | _B6 z6|
_B4_B2 F6 | _B4_B2 F6 | A4A2 c6 | _B4_B2 _B6 |
_B4_B2 _e4_B2 | _B3_B_B2 F6 | _E4_B2 _e3_e_B2 | _B3_B_B2 F6 |
A4A2 A3AF2 | F6 _B6 | _B4 F2 F3F_E2 | D6 z6 |
_B4,_B2, _B6, |  _B4,_B2, _B6, | F4F2 F6 |  _B4,_B2, _B6, |
C4C2 C4C2 |  _B3,_B,_B2, _B6, | C4C2 C3CC2 | _B3,_B,_B2, _B6, |
F4F2 F3FF2 | _B6, -_B6, | F4F2, F3,F,F2, | _B6, z6 |
`,
      opts: {
        viewportHorizontal: true,
        scrollHorizontal: true,
        add_classes: true,
        // responsive: 'resize',
        scale: 1,
      },
      constrolOpts: {
        soundFontUrl: 'https://gleitz.github.io/midi-js-soundfonts/MusyngKite/',
      },
    };
  },
  components: {},
  watch: {
    note(v) {
      const [visualObj] = abcjs.renderAbc('paper', this.note, this.opts);
      this.control.setTune(visualObj, false, this.constrolOpts);
    },
  },
  methods: {},
  mounted() {
    const [visualObj] = abcjs.renderAbc('paper', this.note, this.opts);
    console.log(abcjs);
    const synthControl = new abcjs.synth.SynthController();
    synthControl.load('#main-midi', null, {
      displayRestart: true,
      displayPlay: true,
      displayProgress: true,
      displayLoop: true,
      displayWarp: true,
    });
    this.control = synthControl;
    this.control.setTune(visualObj, false, this.constrolOpts);
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
  background-size: 100% 1.65em;
}
#paper .cursor {
  background-color: #ffffc0;
  opacity: 0.5;
}
#paper {
  /* display: flex;
  justify-content: center; */
}
</style>
