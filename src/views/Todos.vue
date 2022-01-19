<template>
  <div>
    <h2>Todo App</h2>
    <router-link to="/">Home page</router-link>
    <hr>
    <AddTodo
        @add-todo="addTodo"
    />

    <select v-model="filter">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="not-completed">Not completed</option>
      <option value=""></option>
    </select>

    <select v-model="todoItemLimit">
      <option value="3">3</option>
      <option value="5">5</option>
      <option value="7">7</option>
      <option value="10">10</option>
      <option value="50">50</option>
      <option value="100">100</option>
    </select>

    <hr/>

    <Loader
        v-if="loading"
    />
    <TodoList
        v-else-if="filteredTodos.length"
        v-bind:todos="filteredTodos"
        v-bind:limit="setTodoItemLimit"
        @remove-todo="removeTodo"
    />
    <p v-else>No todos!</p>
  </div>
</template>


<script>
import TodoList from '@/components/TodoList'
import AddTodo from '@/components/AddTodo'
import Loader from '@/components/Loader'

export default {
  name: 'App',
  components: {
    TodoList,
    AddTodo,
    Loader
  },
  data() {
    return {
      todos: [],
      loading: true,
      filter: 'all',
      todoItemLimit: 5
    }
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=' + this.setTodoItemLimit)
        .then(response => response.json())
        .then(json => {
          setTimeout(() => {
            this.todos = json
            this.loading = false
          }, 1000)
        })
  },
  // watch: {
  //   setTodoItemLimit(value) {
  //     console.log(value)
  //   }
  // },
  computed: {
    filteredTodos() {
      var filter
      if (this.filter === 'all') {
        filter = this.todos
      }

      if (this.filter === 'completed') {
        filter = this.todos.filter(t => t.completed)
      }

      if (this.filter === 'not-completed') {
        filter = this.todos.filter(t => !t.completed)
      }

      return filter
    },

    setTodoItemLimit() {
      console.log(this.todoItemLimit)
      return this.todoItemLimit
    }
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter(t => t.id !== id)
    },
    addTodo(todo) {
      this.todos.push(todo)
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
