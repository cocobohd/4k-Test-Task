
<template>
  <div class="item" v-if="todos.length > 0"
    v-for="todo in todos" 
    :key="todo.id">
    <h1 class="item--title">{{todo.title}}</h1>
    <label class="switch">
        <input
          v-model = "todo.completed"
          type="checkbox"
          id="check"
          @change="$emit('changeComplete')"
        />
        <span class="slider round"></span>
    </label>
  </div>

  <h2 class="item--message" v-else>
    Oh you dont have any todos...
  </h2>
</template>

<script>
  export default {
    props: {
      todos: {
        type: Array
      }
    },
    emits: ['changeComplete'],
    data() {
      return {
        
      }
    }
}
</script>

<style>
  @import "../../styles/item.css";
</style>