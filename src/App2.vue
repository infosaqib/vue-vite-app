<!-- Options API -->

<script>


export default {
  data() {
    return {
      name: "Saqib",
      status: "active",
      tasks: ["task 1", "task  2", "task 3"],
      link: "https://www.google.com",
    };
  },
  methods: {
    toggleStatus() {
      if (this.status === "active") {
        this.status = "pending";
      } else if (this.status === "pending") {
        this.status = "inactive";
      } else {
        this.status = "active";
      }
    },
  },
};
</script>

<template>
  <h1>Hi</h1>
  <h3>{{ name }} is {{ status }}</h3>
  <!-- <button v-on:click="toggleStatus">Toggle status</button> -->
  <button @click="toggleStatus">Toggle status</button>

  <h2>Tasks</h2>
  <ul>
    <li v-for="task in tasks" :key="task">{{ task }}</li>
  </ul>
  <!-- <a v-bind:href="link">Click for Google</a> <br /> -->
  <a :href="link">Click for Google</a> <br />
</template>

<style scoped>
h1 {
  color: red;
}
</style>
