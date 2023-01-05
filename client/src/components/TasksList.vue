<template>
  <v-card
    variant="outlined"
    v-for="task in propsTask.task"
    :key="task.id"
    class="mb-3 d-flex flex-row align-center pa-2"
  >
    <v-card-text>
      {{ task.title }}
    </v-card-text>
    <v-switch
      label="Done"
      color="success"
      value="success"
      :model-value="task.completed"
      @click="switchTask(task.id, !task.completed)"
    ></v-switch>
    <v-btn color="red" size="small" @click="eraseTask(task.id)">
      <v-icon icon="mdi-delete"></v-icon>
    </v-btn>
  </v-card>
</template>

<script setup>
const propsTask = defineProps({
  task: Array,
});

const emit = defineEmits(["delTask", "changeCompleted"]);

function eraseTask(id) {
  emit("delTask", id);
}

function switchTask(id, completed) {
  emit("changeCompleted", { id, completed });
}
</script>

<style></style>
