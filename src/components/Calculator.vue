<script setup>
import Screen from "../../../tiss/src/components/Screen.vue";
import Keypad from "../../../tiss/src/components/Keypad.vue";
import Log from "@/components/Log.vue";
</script>

<script>


export default {
  name: "Calculator",
  data() {
    return {
      calculation: "",
      expressionArray: [],
      resultArray: []
    };
  },
  methods: {
    input(char) {
      if ((this.calculation[this.calculation.length - 1] === 'r')) {
        this.delete();
      }
      const operators = ['+', '-', '*', '/'];
      const lastChar = this.calculation[this.calculation.length - 1];

      if (operators.includes(char) && (lastChar === ',' || operators.includes(lastChar))) {
        return;
      }
      if (char === '.' && lastChar === '.') {
        return;
      }
      if (char === '.') {
        const lastNumberSegment = this.calculation.split(/[\+\-\*\/]/).pop();
        if (lastNumberSegment.includes('.')) {
          return;
        }
      }
      this.append(char)
    },
    append(a) {
      if(this.calculation.length < 32 ) {this.calculation += a}
    },
    delete() {
      if ((this.calculation[this.calculation.length - 1] === 's')) {
        this.calculation = this.calculation.slice(0, -3);
      } else if ((this.calculation[this.calculation.length - 1] === 'r')) {
        this.calculation = this.calculation.slice(0, -5);
      } else {
        this.calculation = this.calculation.slice(0, -1);
      }

    },
    clear() {
      this.calculation = "";
    },
    invert() {
      if(this.calculation.length === 0 || this.calculation === "Error"){return}
      if (this.calculation.charAt(0) === "-") {
        this.calculation = this.calculation.slice(1);
      } else {
        this.calculation = "-" + this.calculation;
      }
    },
    calculate() {
      if (this.calculation === "Error") {
        throw e
      }
      try {
        let expression = this.calculation
        let calculated = this.calculation = eval(this.calculation.replaceAll('Ans',this.resultArray[this.resultArray.length - 1])).toString();
        this.expressionArray.push(expression.toString())
        this.resultArray.push(calculated.replaceAll('*','x'))
        this.clear()
      } catch (e) {
        this.calculation = "Error";
      }
    }
  },
}
</script>

<template>
  <div class="container">
    <Screen   :displayedString="calculation"/>
    <div class="input-container">
      <Keypad @input="input"
              @calculate="calculate"
              @delete="this.delete"
              @clear="clear"
              @invert="invert"/>
      <Log   :results="resultArray" :expressions="expressionArray"/>
    </div>
    </div>

</template>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  margin: auto;
  flex-shrink: 0;
  width: 50%;
  border: 3px solid dimgray;
  background-color: darkgrey;
  border-radius: 10px;
  padding: 10px;
}
.input-container {
  display: flex;
  flex-direction: row;
}
</style>
