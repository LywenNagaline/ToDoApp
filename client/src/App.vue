<template>
  <v-container>
    <CreateTask @submitTask="createTask"></CreateTask>
  </v-container>

  <v-container>
    <TasksList
      :task="state.tasks"
      @delTask="deleteTask"
      @changeCompleted="changeTask"
    ></TasksList>
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

//AFFICHAGE DES LISTES
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

//SUPPRIMER TÂCHE
async function deleteTask(id) {
  console.log(id);
  await axios.delete(`http://localhost:3000/todos/${id}`, {
    completed: true,
  });
  await fetchTasks();
}

//COMPLETE TÂCHE
async function changeTask(data) {
  console.log(data);
  await axios.patch(`http://localhost:3000/todos/${data.id}`, {
    completed: data.completed,
  });
  await fetchTasks();
}
</script>

<style scoped></style>
