<template>
  <div id="app">
    <h1>Todo App</h1>
    <hr/>
    <TodoList
        v-bind:todos="todos"
    />
  </div>
</template>

<script>
import TodoList from '@/components/TodoList'
export default {
  name: 'App',
  components: {
    TodoList
  },
  data() {
    return {
      todos: [
        {id: 1, title: 'Task 1', completed: false},
        {id: 2, title: 'Task 2', completed: false},
        {id: 3, title: 'Task 3', completed: false}
      ]
    }
  }
}
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
