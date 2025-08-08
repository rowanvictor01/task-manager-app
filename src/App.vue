<script setup>
import { ref, reactive, watch } from "vue";
import Header from "./components/Header.vue";
import TaskList from "./components/TaskList.vue";
import AddTaskForm from "./components/AddTaskForm.vue";

// data
const tasks = reactive([]);
let notif = ref("");

// methods

// watcher to show a notif when a task gets added or removed
watch(
  () => tasks.length,
  (newLength, oldLength) => {
    if (newLength > oldLength) {
      notif.value = "New  task added";
    } else {
      notif.value = "Task deleted";
    }

    setTimeout(() => {
      notif.value = "";
    }, 3000);
  }
);

// watcher to show a notif every time a task is toggled complete
watch(
  () => tasks.map((task) => task.isComplete), // this can be refactored to be in a computed ref and place that property in the source of the watcher
  (newValue, oldValue) => {
    if (
      newValue.length > oldValue.length ||
      newValue.length < oldValue.length
    ) {
      return;
    }

    for (let i = 0; i < newValue.length; i++) {
      if (newValue[i] > oldValue[i]) {
        notif.value = "You've completed a task";
      }
    }

    setTimeout(() => {
      notif.value = "";
    }, 3000);
  },
  { deep: true }
);

function getIndex(taskId) {
  return tasks.findIndex((task) => task.id === taskId);
}

function addTask(task) {
  tasks.push(task);
}

function deleteTask(taskId) {
  const taskIndex = getIndex(taskId);

  const removedTask = tasks.splice(taskIndex, 1);
}

function toggleComplete(taskId) {
  const taskIndex = getIndex(taskId);

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

    <TaskList
      :tasks="tasks"
      @delete-task="deleteTask($event)"
      @toggle-task="toggleComplete($event)"
    />

    <AddTaskForm @get-task="addTask($event)" />

    <div v-if="notif">{{ notif }}</div>
  </main>
</template>

<style scoped></style>
