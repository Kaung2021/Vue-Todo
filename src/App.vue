<template>
  <div id="app">
    <TodoComponents />
  </div>
</template>

<script>
import TodoComponents from "./components/TodoComponents.vue";

export default {
  name: "App",
  components: {
    TodoComponents,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
