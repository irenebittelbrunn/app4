<script setup>
import { ref } from 'vue'

let tarefas = ref([
  'Prova de matemática',
  'Prova de geografia',
  'Trabalho sociologia',
  'Seminário portugues',
  'Seminário educacão fisica',
  'Seminario geografia',
  'Prova de fisica'
])

let item = ref("")

function adicionar() {
  if (item.value.trim()) {
    tarefas.value.push(item.value)
    item.value = ""
  }
}

function deleteTarefa(index) {
  tarefas.value.splice(index, 1)
}
</script>

<template>
  <div class="container">
    <h1>Lista de Tarefas</h1>

    <input type="text" v-model="item"> <br>
    <button @click="adicionar">Confirmar</button>

    <ul>
      <li v-for="(tarefa, index) in tarefas" :key="index">
        <a href="#" @click.prevent="deleteTarefa(index)">Delete</a>
        {{ tarefa }}
      </li>
    </ul>
  </div>
</template>
<style scoped>
input {
  background-color: brown;
  border: none;
  font-size: 2rem;
  border-radius: 50px;
  color: white;
}

button {
  background-color: brown;
  border: none;
  border-radius: 50px;
  font-size: 1.5rem;
  margin: 1vw;
}

h1 {
  font-size: 3rem;
}

ul {
  font-size: 1.5rem;
}
</style>
