<script>
export default {
  data() {
    return {
      numberOne: null,
      numberTwo: null,
      operation: "",
      result: null,
      isOptionInvalid: false,
      isOperationCalculated: false,
      numberRule: (value) => /^\d+$/.test(value) || "Only numbers are allowed",
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
          this.result = parseFloat(this.numberOne) + parseFloat(this.numberTwo);
        } else if (this.operation === "Subtraction") {
          this.result = this.numberOne - this.numberTwo;
        } else if (this.operation === "Multiplication") {
          this.result = this.numberOne * this.numberTwo;
        } else {
          this.result = this.numberOne / this.numberTwo;
        }
        this.isOperationCalculated = true;
      }
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
