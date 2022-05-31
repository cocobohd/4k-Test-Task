<template>
  <div class="mytodos">
    <div class="mytodos--title--search">
      <h1 class="mytodos--title">My todos</h1>
      <input class="mytodos--input" placeholder="Search"/>
    </div>
    <p class="mytodos--nav">All / Done / Not Done</p>
    <div class="todo--items">
      <TodoItem :todos = "todos"/>
    </div>
    <div class="footer"></div>
  </div>
</template>

<script>
  import TodoItem from "./TodoItem.vue"

  export default {
    props: {
      todos: {
        type: Array,
      }
    },
    components: {
      TodoItem
    },
    data() {
      return {

      }
    }
  }
</script>

<style>
  @import "../../styles/mytodos.css";
</style>