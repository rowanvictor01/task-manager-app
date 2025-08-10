<script setup>
import { ref, reactive } from "vue";

const emit = defineEmits(["get-task"]);

let newTask = ref("");
let newDesc = ref("");
let isNewPriority = ref(false);
let idCounter = 1;
let err = ref("");

function getTask() {
  if (!newTask.value) {
    err.value = "No Task Provided";

    setTimeout(() => {
      err.value = "";
    }, 3000);

    return;
  }

  const task = {
    id: idCounter,
    name: newTask.value,
    description: newDesc.value,
    isPriority: isNewPriority.value,
    isComplete: false,
    isEditMode: false,
  };

  // emit after assigning values
  emit("get-task", task);

  idCounter++;

  // reset
  newTask.value = "";
  newDesc.value = "";
  isNewPriority.value = false;
}
</script>

<template>
  <section>
    <form @submit.prevent="getTask">
      <div v-if="err">{{ err }}</div>

      <input placeholder="New Task" v-model="newTask" />

      <label>
        <input type="checkbox" v-model="isNewPriority" />
        Priority
      </label>

      <button type="submit">Add</button>

      <section>
        <textarea
          placeholder="Description (optional)"
          v-model="newDesc"
          rows="3"
        ></textarea>
      </section>
    </form>
  </section>
</template>
