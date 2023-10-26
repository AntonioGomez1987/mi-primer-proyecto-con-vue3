
<template>
  <div class="container text-center mt-3">
    <h1>APP por Jose {{ name.toUpperCase() }}!</h1>
    <br>
    <h2 :class="classCounter">{{ counter }}</h2>
    <br>
    <div class="btn-group">
      <button @click="increment" class="btn btn-success">Aumentar</button>
      <button @click="decrement" class="btn btn-danger">Decrementa</button>
      <button @click="reset" class="btn btn-secondary">Resetear</button>
      <button @click="add" :disabled="bloquearBtnAdd" class="btn btn-primary">Adicionar</button>
    </div>
    <ul class="list-group">
      <li class="list-group-item" v-for="(num, index) in arrayFavoritos" :key="index">
        {{ num }}
      </li>
    </ul>


  </div>
</template>

<script setup>

import { ref, computed } from "vue";

const name = "Vue dinamico";

//metodo - methods
const counter = ref(0);
const arrayFavoritos = ref([]);

const increment = () => {  
  counter.value++;
}

const decrement = () => {
  counter.value--;
}

const reset = () => {
  counter.value = 0;
}

const add = () => {
  arrayFavoritos.value.push(counter.value)
}


const classCounter = computed(() => {
  if (counter.value === 0) {
    return 'zero'
  }
  if (counter.value > 0) {
    return 'positive'
  }
  if (counter.value < 0) {
    return 'negative'
  }
})

const bloquearBtnAdd = computed(() => {
  const numSearch = arrayFavoritos.value.find((num) => num === counter.value)
  console.log(numSearch);
  if (numSearch === 0) return true;
  return numSearch ? true : false;
})
</script>

<style>
h1 {
  color: red;
  text-align: center;
}

.positive {
  color: green;
}

.negative {
  color: red;
}

.zero {
  color: peru
}
</style>