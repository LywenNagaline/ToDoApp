<template>
  <v-card
    variant="outlined"
    v-for="task in propsTask.task"
    :key="task.id"
    class="mb-3"
  >
    <v-card-text>
      {{ task.title }}
    </v-card-text>
  </v-card>
</template>

<script setup>
const propsTask = defineProps({
  task: Array,
});
</script>

<style></style>
