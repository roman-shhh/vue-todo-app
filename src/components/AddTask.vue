<script setup>
import { ref } from 'vue'
import { v4 as uuidv4 } from 'uuid';

const emit = defineEmits(['new-task-added'])

const task = ref('')

const addTask = () => {
  if (task.value.trim()) {
    emit('new-task-added', {
      id: uuidv4(),
      text: task.value.trim(),
      done: false
    })
    task.value = ''
  }
}
</script>

<template>
  <div class="new-task">
    <label for="add-task-input" class="visually-hidden">New task</label>
    <input
      id="add-task-input"
      v-model="task"
      class="task-input"
      placeholder="Add new task"
      @keyup.enter="addTask"
      aria-label="Add new task"
    >

    <button
      class="button-green"
      :disabled="!task"
      @click="addTask"
      aria-label="Add task"
    >
      Add
    </button>
  </div>
</template>