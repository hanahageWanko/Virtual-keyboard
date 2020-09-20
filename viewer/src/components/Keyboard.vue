<template>
  <div class="keyboard">
    <div v-for="(keys, i) in displayKeys" :key="i" class="keyboard--row">
      <button
        v-for="(key, idx) in keys"
        :key="idx"
        :class="keySize(key)"
        @click="inputValues(type, key)"
      >
        <span>{{ key }}</span>
      </button>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";


@Component
export default class Keyboard extends Vue {
  @Prop() private keyarray!: object;
  @Prop() private type!: string;

  textValues: string[] = [];

  public get displayKeys(): object {
    const type = this.type;
    const keys = [...this.keyarray[type], ...this.keyarray["space"]];
    return keys;
  }

  keySize(key): string {
    const defaultClass = "keyboard--key";
    let keySize = "";
    if (key === "enter" || key === "shift") {
      keySize = "option-key";
    }
    if (key === "×") {
      keySize = "option-key backspace-key";
    }
    return defaultClass + " " + keySize;
  }

  inputValues(type, key): void {
    if (key === "enter") key = "\n";
    console.log(key);
    if (key === "shift" || key === "Aa/かな") {
      this.changeKeys(key);
      return;
    }
    if(key === "×") {
      this.$emit("deleteText");
      return;
    }
    if(key === " " && type === "jp") {
      key = "  ";
      console.log(key);
    }
    console.log(key);
    this.textValues.push(key);
    this.$emit("displayvalue", this.textValues.join(""));
  }

  changeKeys(key): void {
    this.$emit("changeKeys", key);
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.keyboard {
  position: fixed;
  left: 0;
  bottom: 0;
  width: 100%;
  padding: 5px 0;
  background: #004134;
  box-shadow: 0 0 50px rgba(0, 0, 0, 0.5);
  user-select: none;
  transition: botom 0.4s;
  padding: 10px;
  box-sizing: border-box;
}

.keyboard--hidden {
  bottom: -100%;
}

.keyboard--row {
  display: flex;
  justify-content: center;
}

.keyboard--row:last-of-type .keyboard--key:first-of-type {
  flex-basis: 12%;
}

.keyboard--row:last-of-type .keyboard--key:last-of-type {
  flex-basis: 60%;
}

.keyboard--key {
  cursor: pointer;
  display: inline-block;
  text-align: center;
  padding: 16px 10px;
  margin: 5px;
  border-radius: 4px;
  background: rgba(3, 104, 84, 0.8);
  color: #fff;
  border: none;
  box-shadow: inset 0px 1px 2px rgba(255, 255, 255, 0.1);
  font-size: 18px;
  width: 60px;
}

.backspace-key span {
  background: #fff;
  color: rgba(3, 104, 84, 0.8);
  padding: 2px 10px;
  position: relative;
}

.backspace-key span::after {
  position: absolute;
  left: -19px;
  top: 50%;
  margin-top: -12px;
  content: "";
  width: 0px;
  height: 0px;
  border-left: 3px solid transparent;
  border-right: 16px solid #fff;
  border-top: 12px solid transparent;
  border-bottom: 12px solid transparent;
}

.option-key {
  flex-basis: 150px;
}
</style>
