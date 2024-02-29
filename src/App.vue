<template>
    <div id="app" class=" min-h-screen flex flex-col items-center justify-center p-6 bg-black">
      <div class="w-full max-w-xs shadow-lg ">
        <h1 class="text-2xl font-bold text-pink-300 text-center mb-6">Simple Calculator</h1>
        <div class="mb-4">
          <input type="number" v-model="number1" class="w-full px-3 py-2 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent" />
        </div>
        <div class="mb-4">
          <select v-model="operation" class="bg-gray-300 text-xl text-pink font-bold w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500">
            <option value="add">+</option>
            <option value="subtract">-</option>
            <option value="multiply">*</option>
            <option value="divide">/</option>
          </select>
        </div>
        <div class="mb-4">
          <input type="number" v-model="number2" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent" />
        </div>
        <div class="mb-6">
          <button @click="performCalculation" class="w-full bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline">
            Calculate
          </button>
        </div>
        <p class="text-center bg-pink-300 font-bold w-full px-3 py-2 rounded-md ">Result: {{ result }}</p>
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
