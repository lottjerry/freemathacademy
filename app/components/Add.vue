<template>
  <div class="flex flex-col items-center justify-center gap-5">
    <h1>Add Two Numbers</h1>
    <form
      @submit.prevent="addNumbers"
      class="flex flex-col items-start justify-start gap-4 text-white"
    >
      <div>
        <label for="num1">First Number:</label>
        <input
          class="text-black"
          type="number"
          v-model="num1"
          id="num1"
          required
        />
      </div>
      <div>
        <label for="num2">Second Number:</label>
        <input
          class="text-black"
          type="number"
          v-model="num2"
          id="num2"
          required
        />
      </div>
      <button type="submit">Add</button>
    </form>

    <div v-if="result !== null">
      <h2 class="text-white">Result: {{ result }}</h2>
    </div>
    <div v-if="error">
      <p class="text-red-600">Error: {{ error }}</p>
    </div>
  </div>
</template>

<script setup>
  import { ref } from 'vue';
  import axios from 'axios';

  const num1 = ref(0);
  const num2 = ref(0);
  const result = ref(null);
  const error = ref(null);

  const addNumbers = async () => {
    try {
      const response = await axios.post('http://127.0.0.1:8000/add', {
        num1: parseFloat(num1.value),
        num2: parseFloat(num2.value),
      });
      result.value = response.data.result;
      error.value = null; // Clear any previous errors
    } catch (err) {
      error.value = 'An error occurred while adding numbers.';
      console.error(err);
    }
  };
</script>
