<template>  
  <div class="todo" v-for="todo in todos">
    <div class="todo_item" v-for="value in todo">
      {{ value }}
      <span @click="removeTodo($index)">X</span>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      newTodo: '',
      picked: ''
    }
  },
  props: {
    todos: '',
    todoTypes: '',
  },
  methods: {
    removeTodo: function (index) {
      this.todos.splice(index, 1);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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

.todo_item {
  padding-left: 10px;
}
</style>
