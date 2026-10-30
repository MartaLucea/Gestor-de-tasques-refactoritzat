<script setup>
import { Tasca } from './models/Tasca'

const props = defineProps({
  tasca: {
    type: Tasca,
    required: true
  }
})

const emit = defineEmits(['marcarTasca', 'borrarTasca'])
</script>

<template>
  <li :class="{ marcada: props.tasca.completada }">
    {{ props.tasca.nom }}
    <small v-show="props.tasca.data">({{ props.tasca.data }})</small>
    <button @click="emit('marcarTasca', props.tasca.id)">
      <span v-if="props.tasca.completada">Desmarcar</span>
      <span v-else>Completar</span>
    </button>
    <button @click="emit('borrarTasca', props.tasca.id)">🗑️</button>
  </li>
</template>

<style scoped>
li {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 2px;
  margin-bottom: 6px;
  border-radius: 6px;
}

li small {
  color: #888;
  margin-left: 10px;
}

button {
  margin-left: 6px;
  padding: 6px 12px;
  border-radius: 6px;
  cursor: pointer;
}

.marcada {
  text-decoration: line-through;
  color: #888;
}
</style>
