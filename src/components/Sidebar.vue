<template>
  <sidebar>
    <div v-for="todoType in todoTypes" @click="filterTodo">
      {{ todoType }}
    <div>
  </sidebar>
</template>

<script>
export default {
  props: {
    todoTypes: '',
    currentTodoType: '',
    filterTodos: '',
    todos: ''
  },
  methods: {
    filterTodo: function (event) {
      this.currentTodoType = event.target.textContent.replace(/(^\s+)|(\s+$)/g, "")
    }
  }
}
</script>

<style scoped>
sidebar {
  flex: 0 0 18rem;
  background-color: rgba(30, 144, 255, 0.9)
}
sidebar div {
  font-size: 1.6rem;
  line-height: 2;
  text-align: center;
  color: #fff;
  cursor: pointer;
}
sidebar div:hover {
  background-color: rgba(0, 0, 0, 0.3)
}
</style>