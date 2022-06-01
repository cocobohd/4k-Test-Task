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
        <MyTodos 
          :todos="todos"
          @change="changeComplete" 
          @all="all"
          @done="sortDone"
          @notDone="sortNotDone"
        />
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
        todos: [],
        allTodos: [],
        doneTodos: [],
        notDoneTodos: []
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
          this.allTodos = data
        }catch {
          console.log("Error")
        }
      },
      all() {
        this.todos = this.allTodos
        this.todos.sort((a,b) => a.completed - b.completed)
      },
      changeComplete() {
        this.todos.sort((a,b) => a.completed - b.completed)
      },
      sortDone() {
        this.doneTodos = this.allTodos.filter(t => t.completed === true)
        this.todos = this.allTodos
        this.todos = this.doneTodos
      },
      sortNotDone() {
        this.notDoneTodos = this.allTodos.filter(t => t.completed === false)
        this.todos = this.allTodos
        this.todos = this.notDoneTodos
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
