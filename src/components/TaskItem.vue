<script setup>
import { reactive } from "vue";

// prop
const { task } = defineProps(["task"]);

// emit
const emit = defineEmits(["delete-task", "toggle-task", "edit-task"]);

// data
const editedTask = reactive({
  name: "",
  description: "",
  isPriority: null,
});

// methods
function runTwoFunctions(task) {
  onEditClick(task);
  setEditTaskPriority(task);
  console.log("Two functions triggered!");
}

function setEditTaskPriority(task) {
  editedTask.isPriority = task.isPriority;
}

function onDeleteClick() {
  emit("delete-task", task.id);
}

function onTaskToggle() {
  emit("toggle-task", task.id);
}

function onEditClick(task) {
  task.isEditMode = true;
}

function onSaveEdit(taskId) {
  editedTask.id = taskId;

  emit("edit-task", editedTask);

  task.isEditMode = false;

  for (let p in editedTask) {
    editedTask[p] = "";
  }
}

function onCancelEdit() {
  task.isEditMode = false;

  for (let p in editedTask) {
    editedTask[p] = "";
  }
}
</script>

<template>
  <section class="task-item">
    <input
      class="toggle-task"
      type="checkbox"
      @click="onTaskToggle"
      :checked="task.isComplete"
      :disabled="task.isEditMode"
    />

    <div>
      <div v-if="!task.isEditMode" class="task-name">
        <span :class="{ complete: task.isComplete }">{{
          task.isPriority ? task.name + "- Priority" : task.name
        }}</span>
      </div>

      <div v-else>
        <input type="text" v-model="editedTask.name" />
        <label>
          Prioritize
          <input type="checkbox" v-model="editedTask.isPriority" />
        </label>
      </div>
      <!-- /task-name -->

      <div v-if="!task.isEditMode">{{ task.description }}</div>

      <textarea v-else v-model="editedTask.description"></textarea>

      <div v-if="!task.isEditMode" class="buttons">
        <button :disabled="task.isComplete" @click="runTwoFunctions(task)">
          Edit
        </button>
        <button @click="onDeleteClick">Delete</button>
      </div>
      <button v-if="task.isEditMode" @click="onSaveEdit(task.id)">Save</button>
      <button v-if="task.isEditMode" @click="onCancelEdit">Cancel</button>
      <!-- /buttons -->
    </div>
  </section>
  <!-- /task-item -->
</template>
