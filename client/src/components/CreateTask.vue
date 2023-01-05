<template>
  <h1>Add List</h1>
  <v-form ref="form">
    <div>
      <v-text-field
        label="Nom de la tâche"
        variant="outlined"
        v-model="taskName"
        required
      >
      </v-text-field>
      <v-btn color="success" class="mr-4" @click="sendList"> Validate </v-btn>
    </div>
  </v-form>
</template>

<script setup>
import { ref } from "vue";

const taskName = ref("");
const taskID = Date.now();

const emit = defineEmits(["submitList"]);

async function sendList() {
  emit("submitList", taskName.value, taskID);
  taskName.value = "";
}
</script>

<style scoped></style>
