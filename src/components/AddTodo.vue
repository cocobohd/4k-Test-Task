<template>
  <div class="addtodo">
    <h1 class="addtodo--title">
      Add todo
    </h1>
    <input 
      v-model.trim="todo.title"
      class="addtodo--input" 
      placeholder="Todo name"
    />
    <button class="addtodo--btn" @click="addTodo()" :class="{'active' : todo.title.length > 0}">+</button>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        todo: {
          title: "",
          completed: false
        }
      }
    },
    methods: {
      addTodo() {
        this.todo.id = Date.now()
        this.$emit("create", this.todo)
        this.todo = {
          title: "",
          completed: false
        }
      }
    }
  }
</script>

<style>
  @import "../styles/addtodo.css";
</style>