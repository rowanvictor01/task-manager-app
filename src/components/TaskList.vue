<script setup>
import TaskItem from "./TaskItem.vue";

const { tasks } = defineProps(["tasks"]);
</script>

<template>
  <section>
    <h2>Tasks</h2>

    <TaskItem
      v-for="(task, index) in tasks"
      :key="task.id"
      :task="task"
      @delete-task="$emit('delete-task', $event)"
      @toggle-task="$emit('toggle-task', $event)"
    />
  </section>
</template>

<style scoped></style>
