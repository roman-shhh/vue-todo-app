<script setup>
defineProps({
  tasks: {
    type: Array,
    required: true,
    default: () => []
  }
})

const emit = defineEmits(['remove-task'])
</script>

<template>
  <div>
    <transition-group name="fade-list" tag="ul" class="task-list">
      <li
        v-for="task of tasks"
        :key="task.id"
        class="task-item"
        @click="task.done = !task.done"
        v-if="tasks.length"
      >
        <div class="task-body" :title="task.text" :class="{'task-done-bg': task.done}">
          <label :for="'done-checkbox-' + task.id" class="visually-hidden">Mark as done</label>
          <input
            class="done-checkbox"
            type="checkbox"
            :id="'done-checkbox-' + task.id"
            :checked="task.done"
            :aria-checked="task.done.toString()"
            :aria-label="task.done ? 'Mark as not done' : 'Mark as done'"
          />

          <div
            class="task-text"
            :class="{'task-done-text': task.done}"
          >
            {{ task.text }}
          </div>
        </div>

        <button
          class="button-red"
          @click="emit('remove-task', task.id)"
          :aria-label="'Remove task: ' + task.text"
        >
          Remove
        </button>
      </li>
    </transition-group>
    <div v-if="!tasks.length" class="empty-list-message">No tasks yet. Add your first task!</div>
  </div>
</template>