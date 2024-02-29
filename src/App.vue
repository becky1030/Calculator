<template>
    <div id="app" class=" min-h-screen flex flex-col items-center justify-center p-6 bg-gradient-to-b from-gray-500">
      <div class="w-full max-w-xs pb-5 px-5 shadow-gray-500 shadow-2xl rounded-xl border-4 border-gray-300">
        <h1 class="text-2xl font-bold text-black text-center mb-3 mt-5">Simple Calculator</h1>
        <div class="mb-4">
          <input type="number" v-model="number1" class="shadow-md shadow-gray-500 w-full px-3 py-2 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent" />
        </div>
        <div class="mb-4">
          <select v-model="operation" class="shadow-md shadow-gray-500 bg-gray-300 text-xl text-pink font-bold w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500">
            <option value="add">+</option>
            <option value="subtract">-</option>
            <option value="multiply">*</option>
            <option value="divide">÷</option>
            <option value="modulus">%</option>
            <option value="exponent">X^y</option>
            <option value="sqrt">√</option>
          </select>
        </div>
        <div class="mb-4">
          <input type="number" v-model="number2" class="shadow-md shadow-gray-500 w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent" />
        </div>
        <div class="mb-6">
          <button @click="performCalculation" class="shadow-md shadow-gray-500 w-full bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline">
            Calculate
          </button>
        </div>
        <p class="text-center bg-orange-400 font-bold w-full px-3 py-2 rounded-md ">Result: {{ result }}</p>
      </div>
    </div>
  </template>

  <script>
  import axios from "axios";

  export default {
    data() {
      return {
        number1: 0,
        number2: 0,
        operation: "add",
        result: null,
      };
    },
    methods: {
      async performCalculation() {
        const response = await fetch("http://localhost:8000/api/calculate", {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify({
            number1: this.number1,
            number2: this.number2,
            operation: this.operation,
          }),
        });
        const data = await response.json();
        this.result = data.result;
      },
    },
  };
  </script>
