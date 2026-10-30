<script setup>
import { ref, computed } from 'vue'

import TaskForm from './components/TaskForm.vue'
import TaskList from './components/TaskList.vue'
import { Tasca } from './components/models/Tasca'

const tasques = ref([])

const missatge = ref('')
let temporitzador = null

function mostrarMissatge(text) {
  missatge.value = text
  clearTimeout(temporitzador)
  temporitzador = setTimeout(() => {
    missatge.value = ''
  }, 2500)
}

function afegirTasca(nom) {
  const nouId = tasques.value.length > 0
    ? tasques.value[tasques.value.length - 1].id + 1
    : 1

  tasques.value.push(new Tasca(nouId, nom))
  mostrarMissatge(`Tasca "${nom}" afegida`)
}

function borrarTasca(id) {
  const index = tasques.value.findIndex(tasca => tasca.id === id)

  if (index !== -1) {
    const [esborrada] = tasques.value.splice(index, 1)
    mostrarMissatge(`Tasca "${esborrada.nom}" eliminada`)
  }
}

function marcarTasca(id) {
  const tasca = tasques.value.find(tasca => tasca.id === id)

  if (tasca) {
    tasca.completada = !tasca.completada
  }
}

const total = computed(() => tasques.value.length)
const pendents = computed(() => tasques.value.filter(tasca => !tasca.completada).length)
const completades = computed(() => total.value - pendents.value)
</script>

<template>
  <div>
    <h1>Gestor de Tasques</h1>
  </div>

  <TaskForm @enviar-tasca="afegirTasca" />

  <p v-if="missatge" class="missatge">{{ missatge }}</p>

  <TaskList
    :tasques="tasques"
    @marcar-tasca="marcarTasca"
    @borrar-tasca="borrarTasca"
  />

  <div>
    <p>Total: {{ total }} | Pendents: {{ pendents }} | Completades: {{ completades }}</p>
  </div>
</template>

<style scoped>
div {
  text-align: center;
  margin: 12px 0;
}

h1 {
  color: #2c3e50;
}

p {
  font-weight: bold;
  color: #2c3e50;
  text-align: center;
}

.missatge {
  color: #2e7d32;
  font-weight: normal;
}
</style>
