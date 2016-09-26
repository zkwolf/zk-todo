<template>
<div id="sidebar">
  <div v-for="value in todoTypes" @click="filterTodo">
    {{ value }}
  <div>
</div>
</template>

<script>
export default {
  name: 'Sidebar',
  props: {
    todoTypes: '',
    todos: ''
  },
  methods: {
    filterTodo: function (event) {
      this.currentTodoType = event.target.textContent.replace(/(^\s+)|(\s+$)/g, "")
      let sidebar = document.querySelector('sidebar')
      for (let todoTypeDiv of sidebar.children) {
        todoTypeDiv.style = 'background-color: none'
      }
      event.target.style = 'background-color: rgba(0, 0, 0, 0.6)'
    }
  }
}
</script>

<style scoped>
#sidebar {
  flex: 0 0 18rem;
  background-color: rgba(30, 144, 255, 0.9)
}
#sidebar div {
  font-size: 1.6rem;
  line-height: 2;
  text-align: center;
  color: #fff;
  cursor: pointer;
}
#sidebar div:hover {
  background-color: rgba(0, 0, 0, 0.3)
}
</style>