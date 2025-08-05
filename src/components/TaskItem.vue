<script setup>
// props
const { task } = defineProps(["task"]);

// emits
const emit = defineEmits(["delete-task"]);

// methods
function onDeleteClick() {
  emit("delete-task", task.id);
}
</script>

<template>
  <section class="task-item">
    <div>{{ task.name }}</div>
    <div>{{ task.description }}</div>
    <button>Edit</button>
    <button @click="onDeleteClick">Delete</button>
  </section>
</template>

<style scoped></style>
