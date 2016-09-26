<template>
  <div id="app">
    <sidebar :todo-types="todoTypes"></sidebar>
    <main>
      <div class="addTodo" @click="addTodoShow = true">+</div>
      <!-- modal -->
      <transition name="modal">
        <div id="modal" v-show="addTodoShow">
          <div id="modal-container">
            <div id="todoError">{{ errorMsg }}</div>
            <div id="todoTypeSelect">
              <div v-for="todoType in todoTypes" class="todoType">
                <input type="radio" v-model="picked" :value="todoType" :id="todoType">
                <label :for="todoType">{{ todoType }}</label>
              </div>
            </div>
            <div id="todoValue">
              <input type="text" v-model="newTodo" @keyup.enter="addTodo" @keyup.esc="addTodoShow = false" id="addTodo">
            </div>
        </div>
      </transition>
      <!-- todoValue -->
      <div class="todo" v-for="(todoUnit, index) in todos">
        <div v-for="todoValue in todoUnit">
          {{ todoValue }}
          <span @click="removeTodo(index)">X</span>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import Sidebar from './components/Sidebar.vue'

export default {
  name: 'Index',
  components: {
    Sidebar
  },
  data () {
    return {
      todos: JSON.parse(localStorage.getItem('todos') || '[]'),
      addTodoShow: '',
      todoTypes: ['All', 'Work', 'Life', 'Study'],
      newTodo: '',
      picked: '',
      errorMsg: ''
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
          this.errorMsg = ''
        }
        else {
          this.errorMsg = 'You must set a todo type'
        }
      }
    },
    removeTodo: function(index) {
      this.todos.splice(index, 1)
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
  html,
  body {
    margin: 0;
    padding: 0;
    height: 100%;
  }
  
  html {
    font-size: 10px;
    font-family: "Roboto", "Helvetica Neue", Arial, sans-serif;
  }
  
  #app {
    display: flex;
    height: 100%
  }
  
  main {
    color: #2c3e50;
    width: 100%;
    padding: 2rem;
  }
  
  main a {
    color: #42b983;
    text-docoration: none;
  }
  
  #todoTypeSelect {
    display: flex;
    margin: 20px 0;
    justify-content: center;
    font-size: 1.4rem;
  }
  
  .addTodo {
    font-size: 3rem;
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
    transition: opacity .7s ease;
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
  
  #todoError {
    font-size: 1.4rem;
    color: #ff4949;
    text-align: center;
  }
  
  #todoTypleSelect {
    display: flex;
    margin-bottom: 14px;
  }
  
  .todoType {
    margin-right: 10px;
  }

  #todoValue {
    display: flex;
    justify-content: center;
  }
  
  input[type="radio"] + label::before {
    content: '\a0';
    display: inline-block;
    vertical-align: .2em;
    width: 1em;
    height: 1em;
    margin-right: .2em;
    border-radius: .2em;
    background: #bfbfbf;
    text-indent: .15em;
    line-height: .65;
    transition: background 1s;
  }
  
  input[type="radio"]:checked + label::before {
    content: '\2713';
    background: #9f9f9f;
    transition: background 1s;
  }
  
  input[type="radio"] {
    position: absolute;
    clip: rect(0, 0, 0, 0);
  }
  
  #addTodo {
    width: 400px;
    line-height: 2rem;
    font-family: monospace;
    padding: 0 0.4rem;
  }
  
  .todo {
    font-size: 1.5rem;
    margin-bottom: .5rem;
  }
  
  .todo span {
    cursor: pointer;
    margin-left: 1rem;
  }
  
  .modal-enter {
    opacity: 0;
  }
  
  .modal-leave-active {
    opacity: 0;
  }
  
  .modal-enter .modal-container,
  .modal-leave-active .modal-container {
    -webkit-transform: scale(1.1);
    transform: scale(1.1);
  }
</style>