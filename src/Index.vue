<template>
	<div id="app">
		<aside>
			<div v-for="(value, index) in todoTypes" :class="{'active': index === selected }" @click="filterTodo(index)">
				{{ value }}
				<div>
		</aside>
		<main>
			<div class="addTodo" @click="addTodoShow = true">+</div>
			<!-- modal -->
			<transition name="modal">
				<div id="modal" v-show="addTodoShow">
					<div id="modal-container">
						<div id="todoTypeSelect">
							<div v-for="todoType in todoTypes" class="todoType">
								<input type="radio" v-model="pickedType" :value="todoType" :id="todoType">
								<label :for="todoType">{{ todoType }}</label>
							</div>
						</div>
						<div id="todoValue">
							<input type="text" v-model="newTodo" @keyup.enter="addTodo" @keyup.esc="addTodoShow = false" id="addTodo" maxLength="40">
						</div>
					</div>
				</div>
			</transition>
			<!-- todoValue -->
			<div class="todo" v-for="todoUnit in filterTodos">
				<div v-for="todoValue in todoUnit[0]">
					{{ todoValue }}
					<div id="completeTodo" @click="removeTodo(todoUnit[1])">X</div>
				</div>
			</div>
		</main>
		</div>
</template>

<script>
export default {
  name: 'Index',
  data () {
    return {
      todos: JSON.parse(localStorage.getItem('todos') || '[]'),
      addTodoShow: '',
      todoTypes: ['All', 'Work', 'Life', 'Study'],
      newTodo: '',
      pickedType: 'All',
      errorMsg: '',
      selected: 0,
    }
  },
  methods: {
    addTodo: function () {
      let text = this.newTodo.trim()
      let pickedType = this.pickedType
      if (text) {
          let todo_item = {}
          todo_item[pickedType] = text
          this.todos.push(todo_item)
          this.newTodo = ''
          this.errorMsg = ''
      }
    },
    removeTodo: function(index) {
      this.todos.splice(index, 1)
    },
    filterTodo: function(index) {
      this.selected = index
    }
  },
  computed: {
    filterTodos: function() {
      let todoUnit = []
      let currentTodoType = this.todoTypes[this.selected]
      if (this.selected == 0) {
        for (let index in this.todos) {
          let todo = this.todos[index]
          todoUnit.push([todo, index])
        }
        return todoUnit
      } else {
        for (let index in this.todos) {
          let todo = this.todos[index]
          if (todo[currentTodoType]) {
            todoUnit.push([todo, index])
          }
        }
        return todoUnit
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
	html,
	body {
		margin: 0;
		padding: 0;
		height: 100%;
	}
	
	html {
		font-size: 10px;
		font-family: Helvetica, Arial, 'Microsoft YaHei', sans-serif;
	}
	
	#app {
		display: flex;
		height: 100%
	}
	
	aside {
		flex: 0 0 18rem;
		background-color: rgba(30, 144, 255, 0.9);
	}
	
	aside div {
		font-size: 1.6rem;
		line-height: 2;
		text-align: center;
		color: #fff;
		cursor: pointer;
	}
	
	aside div:hover {
		background-color: rgba(0, 0, 0, 0.3)
	}
	
	.active {
		background-color: rgba(0, 0, 0, 0.6)
	}
	
	main {
		color: #2c3e50;
		width: 100%;
		padding: 2rem;
		background: #ffe0b2;
	}
	
	main a {
		color: #42b983;
		text-decoration: none;
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
		background: #eeeeee;
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
		padding: 0 0.4rem;
	}
	
	.todo {
		font-size: 1.5rem;
		margin-bottom: .5rem;
	}
	
	#completeTodo {
		display: inline-block;
		cursor: pointer;
		margin-left: 1rem;
		transition: transform .6s;
	}
	
	#completeTodo:hover {
		transform: rotate(180deg);
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