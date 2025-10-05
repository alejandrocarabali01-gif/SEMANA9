<template>
  <div class="container">
    <!-- To Do -->
    <div class="column todo">
      <h3>To Do</h3>
      <ul>
        <li v-for="(tarea, i) in tareas.todo" :key="'todo-'+i">
          {{ tarea }}
          <button @click="$emit('mover', 'todo', 'doing', i)">➡</button>
        </li>
      </ul>
    </div>

    <!-- Doing -->
    <div class="column doing">
      <h3>Doing</h3>
      <ul>
        <li v-for="(tarea, i) in tareas.doing" :key="'doing-'+i">
          {{ tarea }}
          <button @click="$emit('mover', 'doing', 'done', i)">➡</button>
        </li>
      </ul>
    </div>

    <!-- Done -->
    <div class="column done">
      <h3>Done ✅</h3>
      <ul>
        <li v-for="(tarea, i) in tareas.done" :key="'done-'+i">
          {{ tarea }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
defineProps({
  tareas: Object
})
defineEmits(['mover'])
</script>

<style scoped>
.container {
  display: flex;
  justify-content: space-around;
  margin-top: 30px;
  gap: 10px;
}

.column {
  width: 30%;
  background: white;
  border-radius: 10px;
  box-shadow: 0 0 5px rgba(0,0,0,0.1);
  padding: 15px;
}

.todo { border-top: 4px solid #007bff; }
.doing { border-top: 4px solid #28a745; }
.done { border-top: 4px solid #dc3545; }

ul {
  list-style: none;
  padding: 0;
}

li {
  background: #eee;
  padding: 10px;
  margin: 5px 0;
  border-radius: 5px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

button {
  background: #007bff;
  color: white;
  border: none;
  padding: 5px 10px;
  border-radius: 4px;
}
button:hover {
  background: #0056b3;
}
</style>
