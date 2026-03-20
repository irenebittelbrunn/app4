<script setup>
import{ref} from 'vue';
const nome = ref('');
const sobrenome = ref('');
const texto = ref ('');

const nomeCompleto = () => (
  console.log('calculando nome com função')
  return `${nome.value} ${sobrenome.value}`
)
</script>
<template>
 <div class="container">
<input type="text" v-model="nome" placeholder="Nome">
<input type="text" v-model="sobrenome" placeholder="Sobrenome">
<label>{{ nomeCompleto() }}</label>
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
