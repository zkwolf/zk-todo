<template>
  <div class="addTodo" @click="addTodoShow = true">+</div>
  <div class="todo" v-for="todo in todos">
    <div class="todo_item" v-for="value in todo">
      {{ value }}
      <span @click="removeTodo($index)">X</span>
    </div>
  </div>
  <div id="modal" v-show="addTodoShow">
    <div id="modal-container">
      <div v-for="todoType in todoTypes">
        <input type="radio" v-model="picked" value="{{ todoType }}" id="{{ todoType }}">
        <label for="{{ todoType }}">{{ todoType }}</label>
      </div>
      <input type="text" v-model="newTodo" @keyup.enter="addTodo" @keyup.esc="addTodoShow = false" id="addTodo">
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      newTodo: '',
      addTodoShow: false,
      picked: ''
    }
  },
  props: {
    todos: '',
    todoTypes: '',
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
    },
    removeTodo: function (index) {
      this.todos.splice(index, 1);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  #addTodo {
    width: 400px;
    
  }

  .todo {
    font-size: 1.4rem;
    background-color: rgba(0, 0, 0, 0.6);
    line-height: 2;
    width: 100%;
    color: #fff;
  }

  .todo span {
    cursor: pointer;
  }
  .addTodo {
    font-size: 2rem;
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
</style>
