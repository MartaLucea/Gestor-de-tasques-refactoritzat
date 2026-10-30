<script setup>
import { ref, computed } from 'vue'

import TaskItem from './TaskItem.vue'

const props = defineProps({
  tasques: {
    type: Array,
    required: true
  }
})

const emit = defineEmits(['marcarTasca', 'borrarTasca'])

const nomesPendents = ref(false)

const tasquesFiltrades = computed(() => {
  if (nomesPendents.value) {
    return props.tasques.filter(tasca => !tasca.completada)
  }
  return props.tasques
})
</script>

<template>
  <div>
    <label>
      <input type="checkbox" v-model="nomesPendents" />
      Mostra només pendents
    </label>
  </div>

  <div>
    <p v-if="tasquesFiltrades.length === 0">No hi ha tasques per mostrar</p>

    <ul v-else>
      <TaskItem
        v-for="tasca in tasquesFiltrades"
        :key="tasca.id"
        :tasca="tasca"
        @marcar-tasca="emit('marcarTasca', $event)"
        @borrar-tasca="emit('borrarTasca', $event)"
      />
    </ul>
  </div>
</template>

<style scoped>
div {
  text-align: center;
  margin: 12px 0;
}

p {
  font-weight: bold;
  color: #2c3e50;
}

ul {
  padding: 0;
  list-style: none;
}
</style>
