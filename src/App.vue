<template>
  <sidebar :todos="todos" :filter-todos="filterTodos" :todo-types="todoTypes" :current-todo-type.sync="currentTodoType"></sidebar>
  <div id="app">
    <div class="addTodo" @click="addTodoShow = true">+</div>
    <todo :todos="todos" :filter-todos="filterTodos"></todo>
    <div id="modal" v-show="addTodoShow">
      <div id="modal-container">
        <div id="todoTypleSelect">
          <div v-for="todoType in todoTypes">
            <input type="radio" v-model="picked" value="{{ todoType }}" id="{{ todoType }}">
            <label for="{{ todoType }}">{{ todoType }}</label>
          </div>
        </div>
        <input type="text" v-model="newTodo" @keyup.enter="addTodo" @keyup.esc="addTodoShow = false" id="addTodo">
      </div>
    </div>
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
      currentTodoType: 'All',
      todos: JSON.parse(localStorage.getItem('todos') || '[]'),
      addTodoShow: '',
      picked: '',
      newTodo: '',
      filterTodos: []
    }
  },
  computed: {
    filterTodos: function () {
      if (this.currentTodoType === 'All'){
        return this.todos
      }
      let filterTodos = []
      for (let todo of this.todos) {
        if (Object.keys(todo)[0] === this.currentTodoType) {
          filterTodos.push(todo)
        }
      }
      return filterTodos
    }
  },
  methods: {
    addTodo: function () {
      let text = this.newTodo.trim()
      let picked = this.picked
      if (text) {
        if (picked) {
          let todo_item = {}
          todo_item[picked] = text
          this.todos.push(todo_item)
          this.newTodo = ''
        }
      }
    }
  },
  watch: {
    todos: {
      handler: function(todos) {
        localStorage.setItem('todos', JSON.stringify(this.todos))
      },
      deep: true
    }
  }
}
</script>

<style>
html,body {
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

.addTodo {
  font-size: 2rem;
  cursor: pointer;
}

#modal {
  position: fixed;
  z-index: 9999;
  left: 18rem;
  top: 0;
  height: 100%;
  width: calc(100% - 18rem);
  background-color: rgba(0, 0, 0, 0.5);
  transition: opacity .3s ease;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

#modal-container {
  margin: 0 auto;
  padding: 10px;
  width: 500px;
  height: 300px;
  background-color: #fff;
}

#todoTypleSelect {
  display: flex;
  margin-bottom: 20px;
}

#addTodo {
  width: 400px;
}
</style>