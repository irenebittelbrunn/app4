<script setup>
import { ref, computed } from 'vue';

let tarefas = ref([
  { texto: 'Prova Matemática', concluida: false },
  { texto: 'Prova Geografia', concluida: false }
])
let add = ref("")
let aviso = ref(false)
let filtro = ref("todas") 
function adicionar() {
  if (add.value.trim().length < 5) {
    aviso.value = true
    return
  }
  tarefas.value.push({
    texto: add.value,
    concluida: false
  })
  add.value = ""
  aviso.value = false
}
function editarTarefa(tarefa) {
  const edicao = prompt(`Editando ${tarefa.texto}...`)
  if (!edicao || edicao.length < 5) {
    alert("Mínimo 5 caracteres")
    return
  }
  tarefa.texto = edicao
}
function deleteTarefa(tarefa) {
  tarefas.value = tarefas.value.filter(t => t !== tarefa)
}
function toggleConcluida(tarefa) {
  tarefa.concluida = !tarefa.concluida
}
const tarefasFiltradas = computed(() => {
  if (filtro.value === "pendentes") {
    return tarefas.value.filter(t => !t.concluida)
  }
  if (filtro.value === "concluidas") {
    return tarefas.value.filter(t => t.concluida)
  }
  return tarefas.value
})
const pendentes = computed(() =>
  tarefas.value.filter(t => !t.concluida).length
)
const concluidas = computed(() =>
  tarefas.value.filter(t => t.concluida).length
)
</script>
<template>
  <div>
    <h1>Lista de Tarefas</h1>
    <input v-model="add" @keyup.enter="adicionar">
    <button @click="adicionar">Adicionar</button>
    <p v-if="aviso">Mínimo 5 caracteres</p>
    <select v-model="filtro" class="select">
      <option value="todas">Todas</option>
      <option value="pendentes">Pendentes</option>
      <option value="concluidas">Concluídas</option>
    </select>
    <ul>
      <li v-for="tarefa in tarefasFiltradas" :key="tarefa.texto">
        <input type="checkbox" v-model="tarefa.concluida">
        <span :style="{ textDecoration: tarefa.concluida ? 'line-through' : 'none' }">
          {{ tarefa.texto }}
        </span>
        <button @click="editarTarefa(tarefa)">E</button>
        <button @click="deleteTarefa(tarefa)">D</button>
      </li>
    </ul>
    <p>Pendentes: {{ pendentes }}</p>
    <p>Concluídas: {{ concluidas }}</p>
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
option{
  font-size: 1.5rem;
  background-color: brown;
  color: white;
}
p{
  font-size: 1.5rem;
}
.select{
  font-size: 1.5rem;
  background-color: brown;
  color: white;
  border-radius: 50px;
}
</style>
