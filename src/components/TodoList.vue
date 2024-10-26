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

<script lang="ts">
import { defineComponent, PropType } from "vue";
import { Todo } from "../types/Todo";

export default defineComponent({
  props: {
    todoList: {
      type: Array as PropType<Todo[]>,
      required: true,
    },
  },
  emits: ["toggle-todo", "remove-todo", "vaina"],
  setup(_, { emit }) {
    const toggleTodo = (id: number) => emit("toggle-todo", id);
    const removeTodo = (id: number) => emit("remove-todo", id);

    return { toggleTodo, removeTodo };
  },
});
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
