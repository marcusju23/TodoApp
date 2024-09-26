<template>
  <h3>Tasks</h3>
  <ul id="task-list" class="task-list">
    <li v-for="(task, index) in tasks" v-bind:key="task.id">
      <div
          class="task-content"
          @click="task.description ? toggleDescription(index) : null"
          :class="{ 'no-description': !task.description }"
      >
        <span class="task-title">
          <span v-if="task.description" class="description-indicator">🔍</span>
          {{ task.title }}
        </span>
        <span class="task-description" v-show="task.showDescription">{{ task.description }}</span>
      </div>
      <button class="delete-btn" @click="deleteTask(task.id)">X</button>
    </li>
  </ul>
</template>

<script setup>
import {defineProps} from 'vue';

const emit = defineEmits(["taskDeleted"]);

const props = defineProps({
  tasks: {
    type: Array,
    required: true,
  },
});

props.tasks.forEach(task => {
  task.showDescription = false;
});

const toggleDescription = (index) => {
  props.tasks[index].showDescription = !props.tasks[index].showDescription;
};

const deleteTask = (id) => {
  emit("taskDeleted", id);
};
</script>

