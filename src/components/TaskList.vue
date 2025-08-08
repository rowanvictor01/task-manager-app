<script setup>
import { ref, computed } from "vue";
import TaskItem from "./TaskItem.vue";

const { tasks } = defineProps(["tasks"]);

const filter = ref("all");

const incompleteTasks = computed(() => {
  return tasks.filter((task) => !task.isComplete);
});

const priorityTasks = computed(() => {
  return tasks.filter((task) => task.isPriority);
});

const completeTasks = computed(() => {
  return tasks.filter((task) => task.isComplete);
});

function filterTask() {
  if (filter.value === "all") {
    return tasks;
  } else if (filter.value === "incomplete") {
    return incompleteTasks;
  } else if (filter.value === "priority") {
    return priorityTasks;
  } else if (filter.value === "complete") {
    return completeTasks;
  } else {
    return tasks;
  }
}
</script>

<template>
  <section>
    <h2>Tasks</h2>

    <div>
      <select v-model="filter">
        <option disabled>Filter Tasks</option>
        <option value="all">All</option>
        <option value="incomplete">Incomplete</option>
        <option value="priority">Priority</option>
        <option value="complete">Complete</option>
      </select>
    </div>

    <TaskItem
      v-for="task in filterTask()"
      :key="task.id"
      :task="task"
      @delete-task="$emit('delete-task', $event)"
      @toggle-task="$emit('toggle-task', $event)"
    />
  </section>
</template>

<style scoped></style>
