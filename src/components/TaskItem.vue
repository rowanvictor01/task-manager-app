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
    <span>{{ task.name }}</span>
    <span v-if="task.isPriority"> - Priority</span>
    <div>{{ task.description }}</div>

    <button>Edit</button>
    <button @click="onDeleteClick">Delete</button>
  </section>
</template>

<style scoped></style>
