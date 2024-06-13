<script setup>
defineProps({
  tasks: {
    type: Array,
    required: true,
    default: []
  }
})

const emit = defineEmits(['removeTask'])
</script>

<template>
  <ul class="task-list">
    <li
      v-for="task of tasks"
      :key="task.id"
      class="task-item"
      @click="task.done = !task.done"
    >
      <div class="task-body" :title="task.text">
        <input class="done-checkbox" type="checkbox" :checked="task.done" />

        <div
          class="task-text"
          :class="{'task-done-text': task.done}"
        >
          {{ task.text }}
        </div>
      </div>

      <button class="button-red" @click="$emit('removeTask', task.id)">Remove</button>
    </li>
  </ul>
</template>