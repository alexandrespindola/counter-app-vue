<script setup>

import { ref, computed } from 'vue';
const name = "Vue 3";

const counter = ref(0);
const arrayFavoritos = ref([]);

const increment = () => counter.value++

const decrement = () => counter.value--

const reset = () => counter.value = 0

const add = () => {
  arrayFavoritos.value.push(counter.value);
  console.log(arrayFavoritos.value);
}

const blockButtonAdd = computed(() => {
  const numSearch = arrayFavoritos.value.find(num => num === counter.value);
  console.log(numSearch);
  if (numSearch === 0) return true
  return numSearch ? true : false;
})

const classCounter = computed(() => {
  return {
    positive: counter.value > 0,
    negative: counter.value < 0,
    zero: counter.value === 0
  }
})
</script>
<template>
  <div class="hero h-screen flex flex-col justify-center items-center">
    <div class="container bg-green-600 max-w-min items-center justify-center text-white rounded-3xl">
      <div class="flex flex-col justify-between items-center gap-10 p-20">
        <h1 class="text-4xl text-center font-bold">Simple App Vue</h1>
        <h2 class="text-5xl text-center" :class="classCounter">
          {{ counter }}
        </h2>
        <div class="flex flex-row gap-5">
          <button @click="decrement" class="button">Decrement</button>
          <button @click="reset" class="button">Reset</button>
          <button @click="increment" class="button">Increment</button>
          <button @click="add" class="button" :disabled="blockButtonAdd">Add</button>
        </div>
        <div class="container flex flex-col gap-3 items-center">
          <h2 class="text-xl font-medium">Your favorites numbers:</h2>
          <ul class="text-center">
            <li v-for="(num, index) in arrayFavoritos" :key="index">
              {{ num }}
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<style></style>
