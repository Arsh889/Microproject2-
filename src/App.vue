<template>
  <div id="app">

    <img src="@/assets/logo.png" alt="Logo" class="logo">

    <section class="greeting">
      <h2 class="title">
        Hi! How are you, Arshdeep!
      </h2>
    </section>

    <div class="content">
      <h1>My To-Do List</h1>
      <!-- Create a form to add new todos -->
      <form @submit.prevent="addTodo">
        <input type="text" v-model="inputContent" placeholder="Enter your task">
        <button type="submit">Add</button>
      </form>
      <!-- Display the list of todos -->
      <ul>
        <li v-for="(todo, index) in todos" :key="index" :class="{ 'completed': todo.done }">
          <span :class="{ 'completed': todo.done }">{{ todo.content }}</span>
          <button @click="toggleDone(index)">{{ todo.done ? 'Undo' : 'Done' }}</button>
          <button @click="removeTodo(index)">Remove</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

// Define reactive variables
const todos = ref([]);
const inputContent = ref('');

// Function to add a new todo
const addTodo = () => {
  if (inputContent.value.trim() === '') {
    return;
  }

  todos.value.push({
    content: inputContent.value,
    done: false
  });
  inputContent.value = ''; // Clear input field after adding todo
};

// Function to remove a todo
const removeTodo = (index) => {
  todos.value.splice(index, 1);
};

// Function to toggle the "done" status of a todo
const toggleDone = (index) => {
  todos.value[index].done = !todos.value[index].done;
};
</script>

<style>
#app {
  font-family: Arial, sans-serif;
  background-color: #f5d7c7;
  padding: 20px;
}

.content {
  max-width: 600px;
  margin: 0 auto;
}

h1 {
  text-align: center;
}

form {
  margin-bottom: 20px;
}

input[type="text"] {
  width: calc(100% - 70px);
  padding: 8px;
  font-size: 16px;
}

button {
  padding: 8px 16px;
  background-color: #8ef00e;
  color: rgb(185, 59, 243);
  border: none;
  cursor: pointer;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  margin-bottom: 10px;
}

button {
  margin-left: 10px;
}

.logo {
  width: 150px; /* Increase the width to make the logo bigger */
  margin: 20px auto; /* Center the logo horizontally and add some space above and below */
  display: block; /* Ensure the logo behaves as a block element */
}

.completed {
  text-decoration: line-through; /* Apply line-through style to completed todos */
  color: #ccc; /* Dim the color of completed todos */
}
</style>
