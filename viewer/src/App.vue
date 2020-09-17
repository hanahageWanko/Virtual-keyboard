<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <Keyboard :keyarray="boardKey" />
  </div>
</template>

<script lang="ts">
import { Component, Emit, Vue } from "vue-property-decorator";
import Keyboard from "@/components/Keyboard.vue";

@Component({
  components: {
    Keyboard
  }
})
export default class App extends Vue {
  name!: "App";
  // data
  boardKey :{
    "Lowercase": string[][]
    "Uppercase": string[][];
    "Jp": string[][];
    "space": string[][];
  } = {
      "Lowercase":[
        ["1","2","3","4","5","6","7","8","9","0","-","^","×"],
        ["q","w","e","r","t","y","u","i","o","p","@","["],
        ["a","s","d","f","g","h","j","k","l",";",":","]","Enter"],
        ["shift", "z","x","c","v","b","n","m",",",".","?"]
      ],
      "Uppercase":[
        ["!","\"","#","$","%","&","\'","(",")","","=","~","×"],
        ["Q","W","E","R","T","Y","U","I","O","P","p","["],
        ["A","S","D","F","G","H","J","K","L","+","*",":","","Enter"],
        ["shift", "Z","X","C","V","B","N","M","<",">","→","←",""], 
      ],
      "Jp":[
        ["ぬ","ふ","あ","う","え","お","や","ゆ","よ","わ","ほ","へ","×"],
        ["た","て","い","す","か","ん","な","に","ら","せ","",""],
        ["ち","と","し","は","き","く","ま","の","り","れ","け","む","Enter"],
        ["shift", "つ","さ","そ","ひ","こ","み","も","ね","る","め","ろ",""], 
      ],
      "space":[
        ["Aa/かな",""]
      ]
      
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
