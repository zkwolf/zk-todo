<template>
  <sidebar :todo-types="todoTypes"></sidebar>
  <div id="app">
    <todo :todos="todos"></todo>
  </div>
</template>

<script>
import Todo from './components/Todo.vue'
import Sidebar from './components/Sidebar.vue'

export default {
  components: {
    Todo,
    Sidebar
  },
  data () {
    return {
      todoTypes: ['All', 'Work', 'Life', 'Study'],
      todos: []
    }
  }
}
</script>

<style>
html, body {
  margin: 0;
  padding: 0;
  height: 100%;
}

html {
  font-size: 10px;
  font-family: "Roboto", "Helvetica Neue", Arial, sans-serif;
}

body {
  display: flex;
}
#app {
  color: #2c3e50;
  width: 100%;
  padding: 2rem;
}

#app a {
  color: #42b983;
  text-decoration: none;
}

.logo {
  width: 100px;
  height: 100px
}
</style>
