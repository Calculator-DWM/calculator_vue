<script>
import axios from "axios";

export default {
  data() {
    return {
      numberOne: null,
      numberTwo: null,
      operation: "",
      isOptionInvalid: false,
      isOperationCalculated: false,
      operationSymbol: "",
      numberRule: (value) => /^\d+$/.test(value) || "Only numbers are allowed",
      result: null,
    };
  },
  methods: {
    calculate() {
      if (
        this.operation === "" ||
        this.numberOne === null ||
        this.numberTwo === null
      ) {
        this.isOptionInvalid = true;
      } else {
        this.isOptionInvalid = false;
        if (this.operation === "Sum") {
          this.operationSymbol = "+";
        } else if (this.operation === "Subtraction") {
          this.operationSymbol = "-";
        } else if (this.operation === "Multiplication") {
          this.operationSymbol = "*";
        } else {
          this.operationSymbol = "/";
        }
      }

      console.log("Debug");

      const numbers = {
        num1: this.numberOne,
        num2: this.numberTwo,
        operation: this.operationSymbol,
      };

      console.log(numbers);

      axios
        .post(
          "https://calculator-express.onrender.com/calculator/calc",
          numbers
        )
        .then((response) => {
          this.result = response.data.result;
          this.isOperationCalculated = true;
        })
        .catch((error) => console.log(error));
    },
  },
};
</script>

<template>
  <h1>Calculator</h1>
  <div class="calculator">
    <div class="inputs">
      <v-text-field
        v-model.number="numberOne"
        type="number"
        label="Number 1"
        :rules="[numberRule]"
      ></v-text-field>
      <v-text-field
        v-model.number="numberTwo"
        type="number"
        label="Number 2"
        :rules="[numberRule]"
      ></v-text-field>
      <v-select
        v-model="operation"
        label="Operation"
        :items="['Sum', 'Subtraction', 'Multiplication', 'Division']"
      ></v-select>
    </div>
    <v-btn @click="calculate"> Calculate </v-btn>
  </div>
  <div v-if="isOperationCalculated" class="result">
    <h2>{{ this.result }}</h2>
  </div>
  <div v-if="isOptionInvalid" class="alert">
    <h3>Invalid option.</h3>
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
    background-color: lightgreen;
    margin-top: 30px;
  }

  .alert {
    border-radius: 10px;
    padding: 20px;
    background-color: lightcoral;
    margin-top: 30px;
  }
}
</style>
