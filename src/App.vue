<script setup>
import { ref, computed } from "vue";
const name = "Vue 3";
const counter = ref(0);
const color = (value) => {
  if (value < 0) {
    return "color: red";
  }
  if (value > 0) {
    return "color: green";
  } else {
    return "color: none";
  }
};

const classCounter = computed(() => {
  if (counter.value === 0) {
    return "zero";
  }
  if (counter.value > 0) {
    return "positive";
  } else {
    return "negative";
  }
});
const arrayFavoritos = ref([]);

const addFavorites = () => {
  arrayFavoritos.value.push(counter.value);
};

const bloquearBtnAdd = computed(() => {
  const numero = arrayFavoritos.value.find((num) => num === counter.value);
  return numero || numero === 0;
});
</script>

<template>
  <div class="container text-center mt-2">
    <h1>Hola {{ name.toUpperCase() }}</h1>
    <h2 :class="classCounter">{{ counter }}</h2>
    <div class="btn-group">
      <button @click="counter++" class="btn btn-success">Aumentar</button>
      <button @click="counter--" class="btn btn-danger">Disminuir</button>
      <button @click="counter = 0" class="btn btn-secondary">
        Restablecer
      </button>
      <button
        @click="addFavorites"
        :disabled="bloquearBtnAdd"
        class="btn btn-primary"
      >
        Add
      </button>
    </div>
    <br />
    <br />
    <h2>Lista de favoritos</h2>
    <ul class="list-group" v-for="(arrayFavorite, index) in arrayFavoritos" :key="index">
      <li class="list-group-item mt-1">
        {{ arrayFavorite }}
      </li>
    </ul>
  </div>
</template>

<style>
h1 {
  color: rgb(79, 189, 94);
}
.positive {
  color: green;
}
.negative {
  color: red;
}
.zero {
  color: none;
}
</style>
