<template>
  <div>
    <h3>Tasks</h3>

    <ul id="task-list" class="task-list">
      <li v-for="task in tasks" :key="task.id">
        <div class="task-content">
          <span class="task-title">{{ capitalizeTitle(task.title) }}</span>
          <span
              class="task-description"
              :class="{ expanded: expandedTasks[task.id] }"
          >
            {{ task.description }}
          </span>
        </div>

        <div class="task-actions">
          <button class="delete-btn" @click="deleteTask(task.id)">X</button>
          <button v-if="task.description" class="inspect-btn" @click="toggleExpand(task.id)">🔍</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, defineProps } from 'vue';

const emit = defineEmits(["taskDeleted"]);
const props = defineProps({
  tasks: {
    type: Array,
    required: true,
  },
});

const expandedTasks = ref({});

const toggleExpand = (taskId) => {
  expandedTasks.value[taskId] = !expandedTasks.value[taskId];
};

const capitalizeTitle = (title) => {
  if (!title) return '';
  return title.charAt(0).toUpperCase() + title.slice(1);
};

const deleteTask = (id) => {
  emit("taskDeleted", id);
};
</script>
