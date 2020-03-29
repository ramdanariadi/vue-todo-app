<template>
  <div id="app">
    <Logo />
    <TodoList />
    <FooterTodo />
  </div>
</template>

<script>
import Logo from "./components/Logo";
import TodoList from "./components/TodoList";
import FooterTodo from "./components/FooterTodo";

export default {
  name: "App",
  components: {
    TodoList,
    Logo,
    FooterTodo
  }
};
</script>

<style>
#app {
  background-color: aquamarine;
  width: 763px;
  margin: auto;
}
#main-logo {
  margin: auto;
  background-color: black;
}
</style>
