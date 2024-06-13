<script setup>
import { ref, computed } from 'vue'

import AddTask from './components/AddTask.vue'
import ToDosList from './components/ToDosList.vue'

const tasks = ref([])
const filtered = ref(false)

const removeTask = (taskId) => {
  const index = tasks.value.findIndex(task => task.id === taskId)
  tasks.value.splice(index, 1)
}

const removeAll = () => {
  tasks.value = []
}

const hasCompleted = computed(() => {
  return tasks.value.filter(task => task.done).length
})

const removeAllCompleted = () => {
  tasks.value = tasks.value.filter(task => !task.done)
}
</script>

<template>
  <div class="app-container">
    <header>
      <div class="app-title">Your ToDo List</div>
    </header>

    <main>
      <div class="buttons-set">
        <button
          class="button-blue"
          @click="filtered = !filtered"
        >
          {{ filtered ? 'Show All' : 'Show only uncompleted' }}
        </button>
      </div>

      <AddTask @new-task-added="tasks.push($event)" />

      <ToDosList
        :tasks="filtered ? tasks.filter(task => !task.done) : tasks"
        @remove-task="removeTask($event)"
      />

      <div v-if="tasks.length" class="buttons-set">
        <button v-if="tasks.length" class="button-red" @click="removeAll">Remove all</button>
        <button v-if="hasCompleted" class="button-red" @click="removeAllCompleted">Remove all completed</button>
      </div>
    </main>
  </div>
</template>