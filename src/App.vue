<template>
  <div class="todo-container">
    <h1>Vue 3 Todo App</h1>
    <h3>Using Composition API inside Single-File Components (SFCs)</h3>
    <TodoInput @add-todo="addTodo" />
    <TodoList
      :todoList="todos"
      @toggle-todo="toggleTodo"
      @remove-todo="removeTodo"
    />
  </div>
</template>

<script lang="ts" setup>
import { ref } from "vue";
import { Todo } from "./types/Todo";
import { TodoInput, TodoList } from "./components";

const todos = ref<Todo[]>([]);

const addTodo = (text: string) => {
  const newTodo: Todo = {
    id: Date.now(),
    text,
    completed: false,
  };
  todos.value.push(newTodo);
};

const toggleTodo = (id: number) => {
  const todo = todos.value.find((todo) => todo.id === id);
  if (todo) {
    todo.completed = !todo.completed;
  }
};

const removeTodo = (id: number) => {
  todos.value = todos.value.filter((todo) => todo.id !== id);
};
</script>

<style scoped>
.todo-container {
  text-align: center;
  max-width: 500px;
  margin: 0 auto;
}
</style>
