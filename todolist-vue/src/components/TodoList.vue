<template>
  <div>
    <form @submit.prevent="createTodo">
      <input type="text" v-model="newTodo" placeholder="Add a new to-do">
      <button type="submit">Add</button>
    </form>
    <ul>
      <li v-for="todo in todos" :key="todo.id">
        <input type="text" v-model="todo.task" >
        <input type="text" v-model="todo.status" >
        <button @click="updateTodo(todo)">Update</button>
        <button @click="deleteTodo(todo.id)">Delete</button>
      </li>
    </ul>
  </div>
</template>


  
  <script>
  import axios from 'axios'
  
  export default {
    data() {
      return {
        todos: [],
        newTodo: ''
      }
    },
    async created() {
      this.fetchTodos()
    },
    methods: {
      async fetchTodos() {
        const response = await axios.get('/todos')
        this.todos = response.data
      },
      async createTodo() {
        axios.post('/todos', { task: this.newTodo, status: 'incomplete' })
        this.newTodo = ''
        this.fetchTodos()
      },
      async updateTodo(todo) {
        axios.put(`/todos/${todo.id}`, { task: todo.task, status: todo.status })
        this.fetchTodos()
      },
      async deleteTodo(id) {
        axios.delete(`/todos/${id}`)
        this.fetchTodos()
      }
    }
  }
  </script>
  