<template>
  <div>
    <h2>To Do List</h2>
    <div>
      {{uncompletedCount}} of {{todos.length}} remaining
      <button
        @click="onArchiveCompleted"
      >Archive Completed</button>
    </div>
    <br>
    <form @submit.prevent>
      <input
        type="text"
        size="30"
        autofocus
        placeholder="enter new todo here"
        v-model="todoText"
        @change="onTextChange"
      >
      <button :disabled="!todoText" @click="onAddTodo">Add</button>
    </form>
    <ul class="unstyled">
      <li :key="todo.id" v-for="todo in todos">
        <Todo
          :todo="todo"
          :onDeleteTodo="() => onDeleteTodo(todo.id)"
          :onToggleDone="() => onToggleDone(todo)"
        />
      </li>
    </ul>
  </div>
</template>

<script>
/* eslint-disable no-console */
import Todo from './Todo.vue';

let lastId = 0;
const createTodo = (text, done = false) => ({id: ++lastId, text, done});

export default {
  name: 'TodoList',
  components: {Todo},
  computed: {
    uncompletedCount() {
      return this.$data.todos.filter(t => !t.done).length;
    }
  },
  data() {
    return {
      todos: [createTodo('learn Vue', true), createTodo('build a Vue app')],
      todoText: ''
    };
  },
  methods: {
    onAddTodo() {
      this.$data.todos = this.$data.todos.concat(
        createTodo(this.$data.todoText)
      );
      this.$data.todoText = '';
    },

    onArchiveCompleted() {
      this.$data.todos = this.$data.todos.filter(t => !t.done);
    },

    onDeleteTodo(todoId) {
      this.$data.todos = this.$data.todos.filter(t => t.id !== todoId);
    },

    onTextChange(event) {
      this.$data.todoText = event.target.value;
    },

    onToggleDone(todo) {
      const {id} = todo;
      this.$data.todos = this.$data.todos.map(t =>
        t.id === id ? {...t, done: !t.done} : t
      );
    }
  }
};
</script>

<style scoped>
button:disabled {
  background-color: gray;
  color: white;
}

ul.unstyled {
  list-style: none;
  margin-left: 0;
  padding-left: 0;
}
</style>
