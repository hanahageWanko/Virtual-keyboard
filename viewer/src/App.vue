<template>
  <div id="app">
    <textarea
      :value="displayValue"
      cols="30"
      rows="10"
      class="textarea"
    ></textarea>
    <Keyboard
      :keyarray="boardKey"
      :type="type"
      @displayvalue="inputDisplayValue"
      @changeKeys="chengeKeyArray"
      @deleteText="deleteValues"
    />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import Keyboard from "@/components/Keyboard.vue";

@Component({
  components: {
    Keyboard
  }
})
export default class App extends Vue {
  name!: "App";

  // data
  displayValue = "";
  boardKey: {
    lowercase: string[][];
    uppercase: string[][];
    jp: string[][];
    space: string[][];
  } = {
    lowercase: [
      ["1", "2", "3", "4", "5", "6", "7", "8", "9", "0", "-", "^", "×"],
      ["q", "w", "e", "r", "t", "y", "u", "i", "o", "p", "@", "["],
      ["a", "s", "d", "f", "g", "h", "j", "k", "l", ";", ":", "]", "enter"],
      ["shift", "z", "x", "c", "v", "b", "n", "m", ",", ".", "?"]
    ],
    uppercase: [
      ["!", '"', "#", "$", "%", "&", "'", "(", ")", "", "=", "~", "×"],
      ["Q", "W", "E", "R", "T", "Y", "U", "I", "O", "P", "p", "["],
      ["A", "S", "D", "F", "G", "H", "J", "K", "L", "+", "*", ":", "", "enter"],
      ["shift", "Z", "X", "C", "V", "B", "N", "M", "<", ">", "", "", ""]
    ],
    jp: [
      [
        "ぬ",
        "ふ",
        "あ",
        "う",
        "え",
        "お",
        "や",
        "ゆ",
        "よ",
        "わ",
        "ほ",
        "へ",
        "×"
      ],
      ["た", "て", "い", "す", "か", "ん", "な", "に", "ら", "せ", "", ""],
      [
        "ち",
        "と",
        "し",
        "は",
        "き",
        "く",
        "ま",
        "の",
        "り",
        "れ",
        "け",
        "む",
        "enter"
      ],
      [
        "shift",
        "つ",
        "さ",
        "そ",
        "ひ",
        "こ",
        "み",
        "も",
        "ね",
        "る",
        "め",
        "ろ",
        ""
      ]
    ],
    space: [["Aa/かな", " "]]
  };
  type = "lowercase";

  inputDisplayValue(value): void {
    this.displayValue = value;
  }

  chengeKeyArray(key): void {
    const currentType = this.type;
    if (key === "Aa/かな") {
      this.type = currentType === "jp" ? "lowercase" : "jp";
    }
    if (key === "shift") {
      if(this.type === "jp") return;
      this.type = currentType === "lowercase" ? "uppercase" : "lowercase";
    }
  }
  deleteValues():void {
    const nextValue:string = this.displayValue.slice(0, this.displayValue.length -1);
    this.displayValue = nextValue;
  }

}
</script>

<style lang="scss">
@import "./assets/style.css";

html,
body {
  padding: 0;
  margin: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.textarea {
  display: block;
  padding: 10px;
  width: 100%;
  font-size: 120%;
}
</style>
