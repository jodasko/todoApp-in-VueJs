<template>
  <input
    v-model="newTodoText"
    @keyup.enter="handleAddTodo"
    placeholder="Add a new Todo"
  />
</template>

<script lang="ts" setup>
/**
 * There is no need to import defineEmits since they are already globally available when using
 * `<script setup>`.
 * Avoid importing defineEmits in <script setup>.
 * It’s a best practice for clean, concise, and consistent Vue code.
 */
import { ref } from "vue";

const emit = defineEmits<{ (event: "add-todo", newTodoText: string): void }>();

// Reactive state for input text
const newTodoText = ref("");

// Function to emit the new todo text
const handleAddTodo = () => {
  if (newTodoText.value.trim()) {
    emit("add-todo", newTodoText.value); //emit the new todo text
    newTodoText.value = ""; //Clear the input
  }
};
</script>

<style scoped>
input {
  width: 100%;
  padding: 10px;
  font-size: 16px;
}
</style>
