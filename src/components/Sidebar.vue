<template>
  <sidebar>
    <div @click="filterTodo">
      All
    </div>
    <div v-for="todoType in todoTypes" @click="filterTodo">
      {{ todoType }}
    <div>
  </sidebar>
</template>

<script>
export default {
  props: {
    todoTypes: '',
    filterTodos: '',
    todos: ''
  },
  methods: {
    filterTodo: function (event) {
      this.filterTodos = []
      let todoType = event.target.textContent.replace(/(^\s+)|(\s+$)/g, "")
      if (todoType === 'All') {
        this.filterTodos = this.todos
        return
      }
      for (let todo of this.todos) {
        console.log(todoType)
        console.log(Object.keys(todo)[0])
        if (Object.keys(todo)[0] === todoType) {
          this.filterTodos.push(todo)
        }
      }
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
}
</style>