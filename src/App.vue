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
          @searchTodos="searchTodos"
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
        notDoneTodos: [],
        search: ""
      }
    },
    methods: {
      addTodo(todo) {
        this.allTodos.unshift(todo)
        this.todos = this.allTodos
        this.todos.sort((a,b) => a.completed - b.completed)
        localStorage.setItem("Array", JSON.stringify(this.allTodos))
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
      sort() {
        this.todos.sort((a,b) => a.completed - b.completed)
      },
      all() {
        this.todos = this.allTodos
        this.sort()
      },
      changeComplete() {
        this.sort()
        localStorage.setItem("Array", JSON.stringify(this.allTodos))
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
      },
      searchTodos(searchTodo){
        this.todos = this.allTodos
        this.search = searchTodo
        this.todos = this.todos.filter(t => t.title.toLowerCase().includes(this.search.toLowerCase()))
        this.sort()
      }
    },
    mounted() {
      const localArr = JSON.parse(localStorage.getItem("Array"))
      if (localArr !== null ) {
        this.allTodos = localArr
        this.todos = this.allTodos
      }else {
        this.getApi()
      }
      this.sort()
    }
  }
</script>

<style>
@import "./styles/app.css";
@import "./styles/media.css";
</style>
