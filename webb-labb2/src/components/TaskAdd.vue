<template>
  <h3>Add new task</h3>
  <form id="form" @submit.prevent="onSubmit">
    <div class="form-control">
      <h4>Title</h4>
      <input type="text" id="title" v-model="title" placeholder="Enter title..." />
      <h4>Description</h4>
      <textarea type="text" id="description" v-model="description" placeholder="Enter description (optional)..." />
    </div>
    <button class="btn">Add task</button>
  </form>
</template>

<script setup>
import { ref } from 'vue';
import { useToast } from 'vue-toastification';

const toast = useToast();

const emit = defineEmits(["taskSubmitted"]);

const title = ref("");
const description = ref("");

const onSubmit = () => {
  if(!title.value) {
    toast.error("Please enter a title.");
    return;
  }

  const taskData = {
    title: title.value,
    description: description.value,
  }

  emit("taskSubmitted", taskData);

  title.value = "";
  description.value = "";
};
</script>