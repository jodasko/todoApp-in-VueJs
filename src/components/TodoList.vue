<template>
  <ul>
    <li
      v-for="todo in todoList"
      :key="todo.id"
      :class="{ completed: todo.completed }"
    >
      <span @click="toggleTodo(todo.id)">{{ todo.text }}</span>
      <button @click="removeTodo(todo.id)">Delete</button>
    </li>
  </ul>
</template>

<script lang="ts" setup>
/**
 * There is no need to import defineEmits since they are already globally available when using
 * `<script setup>`. Nevertheless I leave it for learning proposal
 * Avoid importing defineEmits in <script setup>.
 * It’s a best practice for clean, concise, and consistent Vue code.
 */
import { defineProps, defineEmits } from "vue";
import { Todo } from "../types/Todo";

// Define props and types
const props = defineProps<{
  todoList: Todo[];
}>();

// Define Emit method
const emit = defineEmits<{
  (e: "toggle-todo", id: number): void;
  (e: "remove-todo", id: number): void;
}>();

// Emit functions
const toggleTodo = (id: number) => emit("toggle-todo", id);
const removeTodo = (id: number) => emit("remove-todo", id);
</script>

<style scoped>
.completed {
  text-decoration: line-through;
  color: gray;
}

li {
  display: flex;
  justify-content: space-between;
  padding: 5px 0;
}

button {
  background-color: red;
  color: white;
  border: none;
  cursor: pointer;
}
</style>
