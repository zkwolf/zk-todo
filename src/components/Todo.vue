<template>
  <span>Add Todo</span>
  <input type="text" v-model="newTodo" @keyup.enter="addTodo">
  <div v-for="todo in todos">
    {{ todo.text }}
    <span @click="removeTodo($index)">X</span>
  </div>
</template>

<script>
export default {
  data () {
    return {
      newTodo: ''
    }
  },
  props: {
    todos: ''
  },
  methods: {
    addTodo: function () {
      let text = this.newTodo.trim()
      if (text) {
        this.todos.push({ text: text })
        this.newTodo = ''
      }
    },
    removeTodo: function (index) {
      this.todos.splice(index, 1);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    input {
        border-radius: 2px;
    }
</style>
