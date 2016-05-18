<template>
  <div class="addTodo" @click="addTodoShow = true">+</div>
  <div class="todo" v-for="todo in todos">
    {{ todo.text }}
    <span @click="removeTodo($index)">X</span>
  </div>
  <div id="modal" v-show="addTodoShow">
    <div id="modal-container">
      <span>Add Todo</span>
      <input type="text" v-model="newTodo" @keyup.enter="addTodo" @keyup.esc="addTodoShow = false">
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      newTodo: '',
      addTodoShow: false
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

  .todo {
    font-size: 1.4rem;
    background-color: rgba(0, 0, 0, 0.6);
    line-height: 2;
    width: 100%;
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
    width: 300px;
    height: 500px;
    background-color: #fff;
  }
</style>
