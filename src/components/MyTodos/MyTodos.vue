<template>
  <div class="mytodos">
    <div class="mytodos--title--search">
      <h1 class="mytodos--title">My todos</h1>
      <input class="mytodos--input" placeholder="Search"/>
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
    props: {
      todos: {
        type: Array,
      }
    },
    emits: ['change','all','done','notDone'],
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