<script setup>
import { ref, reactive } from "vue";
import Header from "./components/Header.vue";
import TaskList from "./components/TaskList.vue";
import AddTaskForm from "./components/AddTaskForm.vue";

// data
const tasks = reactive([]);
let taskDeleteMsg = ref("");

// methods
function addTask(task) {
  tasks.push(task);
}

function deleteTask(taskId) {
  const taskIndex = tasks.findIndex((task) => task.id === taskId);

  if (taskIndex === -1) {
    taskDeleteMsg.value = "Task not found";

    setTimeout(() => {
      taskDeleteMsg.value = "";
    }, 5000);

    return;
  }

  const removedTask = tasks.splice(taskIndex, 1);

  // Task removed notif
  taskDeleteMsg.value = `Task removed`;

  setTimeout(() => {
    taskDeleteMsg.value = "";
  }, 3000);
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

    <AddTaskForm @get-task="addTask($event)" />
    <div v-if="taskDeleteMsg">{{ taskDeleteMsg }}</div>
  </main>
</template>

<style scoped></style>
