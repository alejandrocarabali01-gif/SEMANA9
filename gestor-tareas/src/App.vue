<template>
  <div class="app">
    <h1>Gestor de tareas</h1>

    <div class="input-section">
      <input
        v-model="nuevaTarea"
        @keyup.enter="agregarTarea"
        placeholder="Escribe el nombre de la tarea"
      />
      <button @click="agregarTarea">Agregar</button>
    </div>

    <h2>Listado de tareas</h2>

    <p v-if="!hayTareas" class="no-tasks">No hay tareas registradas.</p>

    <TaskBoard
      v-else
      :tareas="tareas"
      @mover="moverTarea"
    />
  </div>
</template>

<script setup>
import { reactive, ref, computed } from 'vue'
import TaskBoard from './components/TaskBoard.vue'

const nuevaTarea = ref('')
const tareas = reactive({
  todo: [],
  doing: [],
  done: []
})

const hayTareas = computed(() =>
  tareas.todo.length > 0 || tareas.doing.length > 0 || tareas.done.length > 0
)

function agregarTarea() {
  if (nuevaTarea.value.trim() !== '') {
    tareas.todo.push(nuevaTarea.value.trim())
    nuevaTarea.value = ''
  }
}

function moverTarea(origen, destino, index) {
  const tarea = tareas[origen][index]
  tareas[origen].splice(index, 1)
  tareas[destino].push(tarea)
}
</script>

<style>
body {
  background: #f8f9fa;
  color: #333;
  font-family: Arial, sans-serif;
}
.app {
  text-align: center;
  padding: 2rem;
}

.input-section input {
  padding: 10px;
  width: 250px;
  margin-right: 10px;
}

button {
  padding: 10px 15px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}
button:hover {
  background-color: #0056b3;
}

.no-tasks {
  color: gray;
  font-style: italic;
}
</style>
