<template>
  <header class="header--blue">
  </header>

  <main class="main">
    <div class="main--content">

      <h1 class="main--title">
        Todo App
      </h1>

      <div class="main--components">
        <AddTodo @create="addTodo"/>
        <MyTodos v-bind:todos="todos"/>
      </div>

    </div>
  </main>
</template>

<script>
  import AddTodo from "./components/AddTodo.vue"
  import MyTodos from "./components/MyTodos/MyTodos.vue"

  export default {
    components: {
      AddTodo, MyTodos
    },
    data() {
      return {
        todos: []
      }
    },
    methods: {
      addTodo(todo) {
        this.todos.unshift(todo)
      },
      async getApi() {
        try {
          let apiCall = 'https://jsonplaceholder.typicode.com/todos?_limit=20'
          const response = await fetch(apiCall)
          const data = await response.json()
          data.sort((a,b) => a.completed - b.completed)
          this.todos = data
        }catch {
          console.log("Error")
        }
      }
    },
    mounted() {
      this.getApi()
    }
  }
</script>

<style>
@import "./styles/app.css";
</style>
