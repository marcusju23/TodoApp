<template>
  <h4 id="taskAmount">You currently have {{ totalTasks }} unfinished tasks.</h4>
</template>

<script setup>
import {defineProps} from 'vue';

const props = defineProps({
  totalTasks: {
    type: Number,
    required: true,
  },
});
</script>