<template>
  <div id="app">
    <PageHeader />
    <AddToDo v-on:add-todo="addToDo" />
    <ToDos v-bind:todos="todos" v-on:del-todo="deleteToDo" v-on:toggle-complete="toggleComplete" />
  </div>
</template>

<script>
import AddToDo from './components/AddToDo'
import ToDos from './components/ToDos'
import PageHeader from './components/layouts/header'
import axios from 'axios'
 
export default {
  name: 'App',
  components: {
    ToDos,
    PageHeader,
    AddToDo
  },
  data() {
    return {
      todos: []
    }
  },
  methods: {
    deleteToDo(id) {
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      .then(res => {
        this.todos = this.todos.filter(todo => todo.id !== id)
        return res
      })
      .catch(error =>  {
          return Promise.reject(error)
        })
    },
    toggleComplete(todoId) {
      const todo = this.todos.find(todo => todo.id === todoId);
      if (todo) {
        todo.completed = !todo.completed;
      }
    },
    addToDo(newTask) {
      const {title, completed} = newTask
      if (newTask.title === '') {
        alert('Cannot proceed with empty task name.')
        return
      }
      axios.post('https://jsonplaceholder.typicode.com/todos', {
        title,
        completed
      })
      .then(res => this.todos = [...this.todos, res.data])
      .catch(error =>  {
          return Promise.reject(error)
        })
    }
  },
  created() {
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=10')
    .then(res => this.todos = res.data)
    .catch(error =>  {
      return Promise.reject(error)
    })
  }
}
</script>

<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  body {
    font-family: Arial, Helvetica, sans-serif;
  }
  .btn {
    display: inline;
    border: none;
    background: #555;
    color: #fff;
    padding: 7px 20px;
    cursor: pointer;
  }
  .btn:hover {
    background: #666;
  }
</style>
