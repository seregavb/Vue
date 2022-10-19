<template>
  <div id="app">
    <h2>Калькулятор</h2>
    <input type="number" v-model="operand1" />
    <input type="number" v-model="operand2" />

    <p>Результат: {{ result }} </p>

    <button v-on:click="result = Number(operand1) + Number(operand2)">+</button>
    <button v-on:click="result = operand1 - operand2"> - </button>
    <button v-on:click="result = operand1 * operand2"> * </button>
    <button v-on:click="result = operand1 / operand2"> / </button>
    <button v-on:click="result = Math.trunc(operand1 / operand2)"> % </button>
    <button v-on:click="result = Math.pow(operand1, operand2)"> В степень </button>

  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      operand1: '',
      operand2: '',
      result: '',
    }
  }
}
</script>

<style lang="scss">
input {
  padding-left: 10px;
  border-color: rgb(0, 61, 32);
  border-radius: 10px;
  font-family: Arial, Helvetica, sans-serif;
  font-size: 20px;
  background-color: rgb(250, 250, 227);
  text-decoration: none;
}

button {
  margin: 10px;

}
</style>
