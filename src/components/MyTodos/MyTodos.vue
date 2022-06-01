<template>
  <div class="mytodos">
    <div class="mytodos--title--search">
      <h1 class="mytodos--title">My todos</h1>
      <input 
        v-model.trim="searchTodo"
        class="mytodos--input" 
        placeholder="Search" 
        @keyup="search()"
      />
    </div>
    <div class="mytodos--nav">
      <button @click="$emit('all')">All</button>
      <span>/ </span>
      <button @click="$emit('done')">Done</button>
      <span>/ </span>
      <button @click="$emit('notDone')">Not Done</button>
    </div>
    <div class="todo--items">
      <TodoItem :todos = "todos" @changeComplete="$emit('change')"/>
    </div>
    <div class="footer"></div>
  </div>
</template>

<script>
  import TodoItem from "./TodoItem.vue"

  export default {
    methods: {
      search() {
        this.$emit('searchTodos', this.searchTodo)
      }
    },
    data() {
      return {
        searchTodo: ""
      }
    },
    props: {
      todos: {
        type: Array,
      }
    },
    emits: ['change','all','done','notDone', 'searchTodos'],
    components: {
      TodoItem
    },
  }
</script>

<style>
  @import "../../styles/mytodos.css";
</style>