<script setup>
// props
const { task } = defineProps(["task"]);

// emits
const emit = defineEmits(["delete-task", "toggle-task"]);

// methods
function onDeleteClick() {
  emit("delete-task", task.id);
}

function onTaskToggle() {
  emit("toggle-task", task.id);
}
</script>

<template>
  <section class="task-item">
    <input class="toggle-task" type="checkbox" @click="onTaskToggle" />

    <div>
      <div class="task-name">
        <span :class="{ complete: task.isComplete }">{{
          task.isPriority ? task.name + "- Priority" : task.name
        }}</span>
      </div>
      <!-- /task-name -->

      <div class="desc">{{ task.description }}</div>

      <div class="buttons">
        <button :disabled="task.isComplete">Edit</button>
        <button @click="onDeleteClick">Delete</button>
      </div>
      <!-- /buttons -->
    </div>
  </section>
  <!-- /task-item -->
</template>

<style scoped>
section.task-item {
  display: flex;
  /* justify-content: center; */
}

.complete {
  text-decoration: line-through;
}
</style>
