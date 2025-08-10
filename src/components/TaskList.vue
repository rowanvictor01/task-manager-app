<script setup>
import { ref, computed } from "vue";
import TaskItem from "./TaskItem.vue";

// prop
const { tasks } = defineProps(["tasks"]);

// data
const filter = ref("all");

// method
const filteredTasks = computed(() => {
  if (filter.value === "all") {
    return tasks;
  } else if (filter.value === "incomplete") {
    return tasks.filter((task) => !task.isComplete);
  } else if (filter.value === "priority") {
    return tasks.filter((task) => task.isPriority);
  } else if (filter.value === "complete") {
    return tasks.filter((task) => task.isComplete);
  }
});
</script>

<template>
  <section>
    <h2>Tasks</h2>

    <div>
      <label>
        <input type="radio" name="filter" value="all" v-model="filter" />
        All
      </label>

      <label>
        <input type="radio" name="filter" value="incomplete" v-model="filter" />
        Incomplete
      </label>

      <label>
        <input type="radio" name="filter" value="priority" v-model="filter" />
        Priority
      </label>

      <label>
        <input type="radio" name="filter" value="complete" v-model="filter" />
        Complete
      </label>
    </div>

    <TaskItem
      v-for="task in filteredTasks"
      :key="task.id"
      :task="task"
      @delete-task="$emit('delete-task', $event)"
      @toggle-task="$emit('toggle-task', $event)"
      @edit-task="$emit('edit-task', $event)"
    />
  </section>
</template>
