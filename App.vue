<template>
  <div id="app">
    <h2>Калькулятор</h2>
    <input type="number" v-bind:class="{focus: currentEnter == 1}" v-on:click="checkOperand(1)" v-model="operand1" />
    <input type="number" v-bind:class="{focus: currentEnter == 2}" v-on:click="checkOperand(2)" v-model="operand2" />
    =
    <input v-model="result" type="number" class="result" />
    <br>

    <br>
    <label> <input type="checkbox" v-on:click="keyboard" v-bind:checked="keyboardOn" />Показать клавиатуру</label>
    <br>
    <br>

    <div v-if="keyboardOn">
      <button class="keyboard" v-for="num of [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]" v-bind:key="num"
        v-on:click="keyPush(num)">{{num}}</button>
      <button class="keyboard" v-on:click="backspace">
        <= </button>
    </div>

    <div>
      <button class="operandKeys" v-for="operand in operands" v-bind:key="operand" v-on:click="currentOperand=operand">
        {{
        operand }}</button>
    </div>

  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      operand1: '0',
      operand2: '0',
      operands: ['+', '-', '*', '/', '%', '@'],
      currentOperand: '+',
      currentEnter: 1,
      keyboardOn: false,
    }
  },

  methods: {
    add() {
      return Number(this.operand1) + Number(this.operand2)
    },
    substract() {
      return this.operand1 - this.operand2
    },
    multiply() {
      return this.operand1 * this.operand2
    },
    divide() {
      return this.operand1 / this.operand2
    },
    withoutRemainder() {
      return Math.trunc(this.operand1 / this.operand2)
    },
    exponent() {
      return Math.pow(this.operand1, this.operand2)
    },

    calculate(operation) {
      switch (operation) {
        case "+":
          return this.add()
        case "-":
          return this.substract()
        case "*":
          return this.multiply()
        case "/":
          return this.divide()
        case "%":
          return this.withoutRemainder()
        case "@":
          return this.exponent()
      }
    },

    keyboard() {
      this.keyboardOn = !this.keyboardOn
    },
    keyPush(num) {
      if (this.currentEnter == 1) {
        this.operand1 = this.operand1 == 0 ? '' : this.operand1
        this.operand1 = String(this.operand1) + String(num)
      } else if (this.currentEnter == 2) {
        this.operand2 = this.operand2 == 0 ? '' : this.operand2
        this.operand2 = String(this.operand2) + String(num)
      }
    },
    backspace() {
      if (this.currentEnter == 1) {
        this.operand1 = this.operand1.slice(0, -1)
        this.operand1 = this.operand1 == '' ? '0' : this.operand1
      } else if (this.currentEnter == 2) {
        this.operand2 = this.operand2.slice(0, -1)
        this.operand2 = this.operand2 == '' ? '0' : this.operand2
      }
    },
    checkOperand(numberOperand) {
      this.currentEnter = numberOperand
    },
  },

  computed: {
    result() {
      return this.calculate(this.currentOperand)
      // return this.result = Number(this.operand1) + Number(this.operand2)
    }
  },

}
</script>



<style lang="scss">
input {
  padding-left: 10px;
  border-color: rgb(175, 175, 175);
  border-radius: 10px;
  font-family: Arial, Helvetica, sans-serif;
  font-size: 20px;
  background-color: rgb(250, 250, 227);
}

.operandKeys {
  margin-right: 8px;
  margin-bottom: 20px;
  width: 40px;
  height: 40px;
  background-color: rgb(75, 75, 75);
  color: white;
  font-size: 14px;
  font-weight: 800;
  border-radius: 10px;
}

.result {
  background-color: rgb(221, 216, 169);
}

.keyboard {
  background-color: rgb(206, 206, 206);
  color: black;
  margin-right: 4px;
  margin-bottom: 20px;
  padding: 6px 10px;
  font-size: 16px;
  font-weight: 500;
}

.focus {
  box-shadow: 0px 5px 10px 0px rgba(0, 0, 0, 0.5)
}
</style>
