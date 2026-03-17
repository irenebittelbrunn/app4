<script setup>
import { ref } from 'vue';
let tarefas = ref([
  'Prova Matemática',
  'Prova Geografia',
  'Trabalho Sociologia',
  'Seminário Português',
  'Seminário Educação Física',
  'Seminário Geografia',
  'Prova Física'
])
let aviso = ref(false);
let add = ref("")
function adicionar() {
  if (add.value.length < 5) {
  } else {
    if (add.value.trim()) {
      tarefas.value.push(add.value);
      aviso.value = false
      add.value = ""
    }
  }
}

function editarTarefa(item) {
  const pos = tarefas.value.indexOf(item);
  const edicao = prompt(`Editando ${item}...`);
  if (edicao.length < 5) {
    alert("Insira no mínimo 5 caracteres")
  } else {
    tarefas.value.splice(pos, 1, edicao);
  }


}

function deleteTarefa(item) {
  const pos = tarefas.value.indexOf(item);
  tarefas.value.splice(pos, 1);
}


</script>

<template>
  <div class="container">
    <h1>Lista de Tarefas</h1>
    <input type="text" v-model="add" @keyup.enter="adicionar">
    <button @click="adicionar">CONFIRMAR</button>
    <p v-show="aviso">Insira no mínimo 5 caracteres</p>
    <ul>
      <li v-for="tarefa in tarefas" :key="tarefa">
        <a href="#" @click.prevent="editarTarefa(tarefa)">E</a>
        <a href="#" @click.prevent="deleteTarefa(tarefa)">D</a>
        {{ tarefa }}
      </li>
    </ul>
    <button @click="tarefas.sort()">Ordenar</button>
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
