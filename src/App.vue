<script setup>
  import { ref, computed } from "vue";

  const name = 'Dynamic Vue.js + Bootstrap 5';

  let counter = ref(0);
  let favNumbers = ref([]);

  const increment = () => {
    counter.value++;
  }

  const decrement = () => {
    counter.value--;
  }

  const reset = () => {
    counter.value = 0;
  }

  const classComputed = computed(() => {
    if (counter.value === 0) {
      return 'zero';
    }

    if (counter.value < 0) {
      return 'negative';
    }

    if (counter.value > 0) {
      return 'positive';
    }
  })

  const addNumber = () => {
    favNumbers.value.push(counter.value);
  }

  const emptyList = () => {
    favNumbers.value = [];
  }

  const isRepeatedNumber = computed(() => {
    return (favNumbers.value.indexOf(counter.value) !== -1);
  })
</script>

<template>
  <!-- Using Bootstrap 5 -->
  <div class="container text-center mt-3">
    <h1> {{ name.toUpperCase() }} </h1>
    <br/>
    <h2 :class="classComputed"> {{ counter }} </h2>
    <br/>
    <div class="btn-group">
      <button @click="increment" class="btn btn-success"> Increment </button>
      <button @click="decrement" class="btn btn-danger"> Decrement </button>
      <button :disabled="isRepeatedNumber" @click="addNumber" class="btn btn-primary"> Add number </button>
      <button @click="reset" class="btn btn-secondary"> Reset counter </button>
      <button @click="emptyList()" class="btn btn-dark"> Empty list </button>
    </div>
    <ul class="mt-4 list-group list-group-flush">
      <li class="list-group-item" v-for="(num, index) in favNumbers" :key="index"> {{ num }} </li>
    </ul>
  </div>
</template>

<style>
  h1 {
    color: dodgerblue;
  }

  .positive {
    color: green;
  }

  .negative {
    color: red;
  }

  .zero {
    color: peru;
  }
</style>
