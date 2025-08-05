<script setup>
import TaskItem from "./TaskItem.vue";

const { tasks } = defineProps(["tasks"]);
</script>

<template>
  <section>
    <TaskItem
      v-for="(task, index) in tasks"
      :key="task.id"
      :task="task"
      @delete-task="$emit('delete-task', $event)"
    />
  </section>
</template>

<style scoped></style>
