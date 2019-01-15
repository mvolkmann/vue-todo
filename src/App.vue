<template>
  <div id="app">
    <TodoList/>
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue';

export default {
  name: 'app',
  components: {
    TodoList
  }
};
</script>

<style>
#app {
  font-family: sans-serif;
  padding-left: 10px;
}
</style>
