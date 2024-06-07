<script setup lang="ts">
import { ref } from "vue";
import { Todo } from "@/models/Todo";

const addTodo = () => {
  todos.value.push(new Todo(todoText.value));
  todoText.value = "";
};

const removeTodo = (i: number) => {
  todos.value.splice(i, 1);
};

const toggleTodo = (i: number) => {
  todos.value[i].done = !todos.value[i].done;
};

const handleInput = (e: any) => {
  todoText.value = e.target.value;
};

const todos = ref<Todo[]>([]);
const todoText = ref("");
</script>

<template>
  <div>
    <input type="text" :value="todoText" @input="handleInput" />
    <button @click="addTodo">Spara</button>
  </div>

  <ul>
    <li v-for="(todo, i) in todos" :key="todo.id">
      <span :class="todo.done ? 'done' : ''">{{ todo.text }}</span>
      <button @click="() => toggleTodo(i)">Ändra</button>
      <button @click="() => removeTodo(i)">Ta bort</button>
    </li>
  </ul>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
