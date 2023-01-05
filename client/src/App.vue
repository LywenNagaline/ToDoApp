<template>
  <v-container>
    <CreateTask @submitTask="createTask"></CreateTask>
  </v-container>

  <v-container>
    <TasksList :task="state.tasks"></TasksList>
  </v-container>
</template>

<script setup>
import CreateTask from "./components/CreateTask.vue";
import TasksList from "./components/TasksList.vue";
import { reactive, onMounted } from "vue";
import axios from "axios";

// CREATION DES LISTES
async function createTask(taskName, taskID) {
  await axios.post("http://localhost:3000/todos", {
    id: taskID,
    title: taskName,
    completed: false,
  });
  await fetchTasks();
}

onMounted(() => {
  fetchTasks();
});

const state = reactive({
  tasks: {},
});

async function fetchTasks() {
  const response = await axios.get("http://localhost:3000/todos");
  state.tasks = response.data;
}
</script>

<style scoped></style>
