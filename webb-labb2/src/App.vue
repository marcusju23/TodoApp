<template>
  <Header></Header>
  <div class="container">
    <TaskAmount :totalTasks="totalTasks"/>
    <TaskList :tasks="tasks" @taskDeleted="handleTaskDeleted"/>
    <TaskAdd @taskSubmitted="handleTaskSubmitted"/>
  </div>
</template>

<script setup>
import Header from './components/Header.vue';
import TaskAmount from "./components/TaskAmount.vue";
import TaskList from "./components/TaskList.vue";
import TaskAdd from "./components/TaskAdd.vue";

import {ref, computed, onMounted} from 'vue';

import {useToast} from 'vue-toastification';

const toast = useToast();

const tasks = ref([]);

onMounted(() => {
  const savedTasks = JSON.parse(localStorage.getItem("tasks"));

  if (savedTasks) {
    tasks.value = savedTasks;
  }
});

/*          Get total tasks         */
const totalTasks = computed(() => {
  return tasks.value.length;
});

/*          Add task          */
const handleTaskSubmitted = (taskData) => {
  tasks.value.push({
    id: generatedUniqueId(),
    title: taskData.title,
    description: taskData.description
  })

  saveTasksToLocalStorage();
  toast.success("Task added successfully.");
};

/*          Generate unique ID          */
const generatedUniqueId = () => {
  return Math.floor(Math.random() * 100000);
};

/*          Delete task         */
const handleTaskDeleted = (id) => {
  tasks.value = tasks.value.filter((task) => task.id !== id);

  saveTasksToLocalStorage();
  toast.success("Task deleted successfully.");
};

/*          Save to LocalStorage          */
const saveTasksToLocalStorage = () => {
  localStorage.setItem("tasks", JSON.stringify(tasks.value));
};
</script>