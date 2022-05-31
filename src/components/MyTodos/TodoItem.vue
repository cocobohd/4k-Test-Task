
<template>
  <div class="item" v-for="todo in todos">
    <h1 class="item--title">{{todo.title}}</h1>
    <label class="switch">
        <input
          v-model = "todo.completed"
          type="checkbox"
          id="check"
        />
        <span class="slider round"></span>
    </label>
  </div>
</template>

<script>
  export default {
    props: {
      todos: {
        type: Array
      }
    },
    data() {
      return {
        
      }
    }
}
</script>

<style>
  @import "../../styles/item.css";
</style>