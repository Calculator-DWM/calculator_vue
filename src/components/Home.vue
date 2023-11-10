<script>
export default {
  data() {
    return {
      numberOne: null,
      numberTwo: null,
      operation: "",
      result: null,
    };
  },
  methods: {
    calculate() {
      console.log(this.numberOne);
      console.log(this.numberTwo);
      console.log(this.operation);
      if (this.operation === "Sum") {
        this.result = parseFloat(this.numberOne) + parseFloat(this.numberTwo);
      } else if (this.operation === "Subtraction") {
        this.result = this.numberOne - this.numberTwo;
      } else if (this.operation === "Multiplication") {
        this.result = this.numberOne * this.numberTwo;
      } else {
        this.result = this.numberOne / this.numberTwo;
      }
    },
  },
};
</script>

<template>
  <h1>Calculator</h1>
  <div class="calculator">
    <div class="inputs">
      <v-text-field v-model="numberOne" label="Number 1"></v-text-field>
      <v-text-field v-model="numberTwo" label="Number 2"></v-text-field>
      <v-select
        v-model="operation"
        label="Operation"
        :items="['Sum', 'Subtraction', 'Multiplication', 'Division']"
      ></v-select>
    </div>
    <v-btn @click="calculate"> Calculate </v-btn>
  </div>
  <div class="result">
    <h2>{{ this.result }}</h2>
  </div>
</template>

<style scoped>
@media only screen and (min-width: 320px) {
  .calculator {
    /* background-color: lightcoral; */
    display: flex;
    flex-direction: column;
  }

  .inputs {
    margin-top: 30px;
  }

  .result {
    border-radius: 10px;
    padding: 20px;
    background-color: lightcoral;
    margin-top: 30px;
  }
}
</style>
