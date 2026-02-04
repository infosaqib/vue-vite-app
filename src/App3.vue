<!-- Composition API -->

<script setup>
import { onMounted, ref } from "vue";

const name = ref("Hafiz");
const status = ref("pending");
const tasks = ref('');
const newTask = ref("");

const toggleStatus = () => {
  if (status.value === "active") {
    status.value = "pending";
  } else if (status.value === "pending") {
    status.value = "inactive";
  } else {
    status.value = "active";
  }
};

const addTask = () => {
  if (newTask.value.trim() !== "") {
    tasks.value.push(newTask.value);
    newTask.value = "";
  }
};

const deleteTask = (index) => {
  tasks.value.splice(index, 1);
};

onMounted(async () => {
  try {
    const response = await fetch('https://dummyjson.com/todos');
    const data = await response.json();
    tasks.value = data.todos.map((task) => task.todo);
  } catch (error) {
    console.error("Error fetching tasks");
  }
});
</script>

<template>
  <h1>Hi Folks!</h1>
  <h3>{{ name }} is {{ status }}</h3>
  <!-- <button v-on:click="toggleStatus">Toggle status</button> -->
  <button @click="toggleStatus">Toggle status</button>

  <h2>Tasks</h2>
  <ul>
    <li v-for="(task, index) in tasks" :key="task">
      <span> {{ task }}</span>
      <button @click="deleteTask(index)">x</button>
    </li>
  </ul>

  <form @submit.prevent="addTask">
    <label for="newTask">Add Task</label>
    <input type="text" name="newTask" id="newTask" v-model="newTask" />
    <button type="submit">Submit</button>
  </form>
</template>

<style scoped>
h1 {
  color: red;
}
</style>
