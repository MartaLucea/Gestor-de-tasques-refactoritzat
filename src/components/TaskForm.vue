<script setup>
import { ref } from 'vue'

const emit = defineEmits(['enviarTasca'])

const tasca = ref('')

function enviarTasca() {
  const nom = tasca.value.trim()
  if (!nom) return

  emit('enviarTasca', nom)
  tasca.value = ''
}
</script>

<template>
  <div>
    <input
      v-model="tasca"
      placeholder="Escriu una nova tasca"
      @keyup.enter="enviarTasca"
    />
    <button @click="enviarTasca">Afegir</button>
  </div>
</template>

<style scoped>
div {
  text-align: center;
  margin: 12px 0;
}

input {
  padding: 6px 10px;
  border: 2px solid #b8c4d6;
  border-radius: 6px;
}

button {
  margin-left: 6px;
  padding: 6px 12px;
  border-radius: 6px;
  cursor: pointer;
}
</style>
