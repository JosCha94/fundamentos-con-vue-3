<script setup>
import { ref, computed } from "vue";
const name = "Practica Fundamentos de VUE";
let edad = ref(0);
const arrayEdad = ref([]);

const aumentar = () => {
  edad.value++;
};

const disminuir = () => {
  edad.value--;
};
const reset = () => {
  edad.value = 0;
};
const add = () => {
  arrayEdad.value.push(edad.value);
};

const colorEdad = computed(() => {
  if (edad.value === 0) {
    return "zero";
  }
  return edad.value > 0 ? "positive" : "negative";
});

const bloquear = computed(() => {
  const number = arrayEdad.value.find((num) => num === edad.value);
  return number || number === 0;
});
</script>

<template>
  <div class="row my-2 text-center">
    <div class="col-12 mb-2 text-danger ">
      <h1>{{ name.toUpperCase() }}</h1>
    </div>
    <div class="col-12">
      <h2 class="my-3">
        Edad: <span :class="colorEdad">{{ edad }}</span>
      </h2>

      <button @click="aumentar" class="btn btn-success">Aumentar</button>
      <button @click="reset" class="btn btn-warning">Resetear</button>
      <button @click="disminuir" class="btn btn-danger">Disminuir</button>
      <button @click="add" :disabled="bloquear" class="btn btn-primary">Agregar</button>
    </div>
    <div class="col-12 my-4">
        <h4 class="text-center">Array de Edades</h4>
      <ul class="list-group">
        <li class="list-group-item" v-for="(item, index) in arrayEdad" :key="index">
          {{ item }}
        </li>
      </ul>
    </div>
  </div>

  <hr />
</template>

<style scoped>
.negative {
  color: red;
}

.positive {
  color: green;
}

.zero {
  color: blue;
}
</style>
