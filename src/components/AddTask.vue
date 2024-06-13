<script setup>
import { ref } from 'vue'
import { v4 as uuidv4 } from 'uuid';

const emit = defineEmits(['newTaskAdded'])

const task = ref('')

const addTask = () => {
  if (task.value.trim()) {
    emit('newTaskAdded', {
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
    <input
      v-model="task"
      class="task-input"
      placeholder="Add new task"
      @keyup.enter="addTask"
    >

    <button
      class="button-green"
      :disabled="!task"
      @click="addTask"
    >
      Add
    </button>
  </div>
</template>