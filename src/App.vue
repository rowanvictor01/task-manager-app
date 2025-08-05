<script setup>
import { ref, reactive } from "vue";
import Header from "./components/Header.vue";
import TaskList from "./components/TaskList.vue";

// data
const tasks = reactive([]);
const newTaskName = ref("");
const newTaskDesc = ref("");
let idCounter = 1;

// methods
function addTask() {
  const task = {
    id: idCounter,
    name: newTaskName.value,
    description: newTaskDesc.value,
    isPriority: false,
    isComplete: false,
  };

  tasks.push(task);
  idCounter++;

  newTaskName.value = "";
  newTaskDesc.value = "";
}

function deleteTask(taskId) {
  const taskIndex = tasks.findIndex((task) => {
    task.id === taskId;
  });

  const removedTask = tasks.splice(taskIndex, 1);

  // Task removed notif
  console.log(`Task ${removedTask} was removed`);
}

function toggleComplete(taskId) {
  if (tasks[taskIndex].isComplete) {
    tasks[taskIndex].isComplete = false;
  } else {
    tasks[taskIndex].isComplete = true;
  }
}

function editTask() {
  // will think about it
}
</script>

<template>
  <main>
    <Header />

    <TaskList :tasks="tasks" @delete-task="deleteTask($event)" />

    <section class="form"></section>
  </main>
</template>

<style scoped></style>
