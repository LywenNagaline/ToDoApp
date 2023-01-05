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
    <v-btn color="red" size="small" @click="eraseTask(task.id)">
      <v-icon icon="mdi-delete"></v-icon>
    </v-btn>
  </v-card>
</template>

<script setup>
const propsTask = defineProps({
  task: Array,
});

const emit = defineEmits(["delTask"]);

function eraseTask(id) {
  emit("delTask", id);
}
</script>

<style></style>
