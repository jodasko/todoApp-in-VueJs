<template>
  <input
    v-model="newTodoText"
    @keyup.enter="handleAddTodo"
    placeholder="Add a new Todo"
  />
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";

export default defineComponent({
  emits: ["add-todo"],
  setup(_, { emit }) {
    const newTodoText = ref("");

    const handleAddTodo = () => {
      if (newTodoText.value.trim()) {
        emit("add-todo", newTodoText.value); //emit the new todo text
        newTodoText.value = ""; //Clear the input
      }
    };

    return {
      newTodoText,
      handleAddTodo,
    };
  },
});
</script>

<style scoped>
input {
  width: 100%;
  padding: 10px;
  font-size: 16px;
}
</style>
