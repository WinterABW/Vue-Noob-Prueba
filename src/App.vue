<script setup>
import { ref, computed } from 'vue'

const name = "Vue dinamico";
const styleColor = "color:blue";
const arrayColors = ["blue", "red", "green"];
const act = false;
const arrayNames = ["Victor", "Luis", "Isaac", "Pablo"];
const objetoPersona = {
  name: "Winter",
  edad: 21,
  isMerried: true,
  id: 1,
};
const handleClick = (mensaje) => console.log(`click ${mensaje}`);

const counter = ref(0);

const aumentarCounter = () => counter.value++
const disminuirContador = () => counter.value--
const resetear = () => counter.value = 0

const classComputed = computed(() => {
  if (counter.value == 0) {
    return 'zero'
  }
  if (counter.value < 0) {
    return 'negativo'
  }
  if (counter.value > 0) {
    return 'posit'
  }
});
const a = setInterval(resetear, 60000)


const arrayNum = ref([])
const add = () => arrayNum.value.push(counter.value);

const block = computed(() => {
  const searchNum = arrayNum.value.find((num) => num === counter.value);
  return searchNum || searchNum === 0;
});
</script>

<template>
<div class="container">
  <h1>hola con mi {{name.toLocaleUpperCase()}} </h1>
  <h2>{{arrayColors}}</h2>
  <p :style="`color:${arrayColors[0]}`">Hey, parrafo azul</p>
  <p v-if="act">Estoy activo</p>
  <p v-else>Estoy inactivo</p>
  <ul class="list-group">
    <li v-for="(name,index) in arrayNames" :key="index" class="list-group-item">{{index}}-{{name}}</li>
  </ul>
  <ul class="list-group">
    <template v-for="(valor, nombreDeLaPropiedad, index) in objetoPersona" :key="valor">
      <li v-if="objetoPersona.isMerried" class="list-group-item">{{index}} - {{nombreDeLaPropiedad}}: {{valor}}</li>
    </template>
  </ul>
</div>
  
<div class="container text-center">
  <h2 :class="classComputed">{{counter}}</h2>
  <div class="btn-group">
    <button @click.left.prevent="handleClick('Izquierdo')">Click Izquierdo</button>
    <button @click.right.prevent="handleClick('Derecho')">Click Derecho</button>
    
    
    <br><br>
    <button @click="aumentarCounter" class="btn btn-success">Aumentar</button>
    <button @click="disminuirContador" class="btn btn-danger">Disminuir</button>
    <button @click="resetear" class="btn btn-secondary">Resetear</button>
    <button @click="add" :disabled="block" class="btn btn-primary">Add</button>
      </div>
      <ul class="list-group">
        <li v-for="item in arrayNum" :key="item" class="list-group-item">
          {{item}}
        </li>
      </ul>
  </div>
  
</template>

<style>
h1 {
  color: blueviolet;
}

.posit {
  color: green;
}

.negativo {
  color: red;
}
</style>
