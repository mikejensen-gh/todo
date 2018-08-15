<template>
<div class="todo">
  <div id="todoControls">
    <button id="addTodo" v-on:click="addNewTodo">Add new todo</button>
    <button id="deleteAllTodos" @click="deleteAllTodos">Remove all todos</button>
  </div>
  <div id="todoList">
<!--     <ul id="todos">
      <li
        v-for="todo in todos"
        :key="todo.id"
        :class="{ solved: todo.solved }"
      >
        {{ todo.title }}
        <button id="solveTodo" @click="solveTodo(todo.id)">-</button>
        <button id="deleteTodo" @click="deleteTodo">x</button>
      </li>
    </ul> -->
    <ul id="todos">
      <li
        v-for="(todo, index) in unsolvedTodos"
        :key="todo.id"
        :class="{ solved: todo.solved }"
      >
        Title: {{ todo.title }} {{ todo.id }} Index: {{ index }} Solved: {{ todo.solved }}
        <button id="solveTodo" @click="solveTodo(index)">-</button>
        <button id="deleteTodo" @click="deleteTodo">x</button>
      </li>
      <li
        v-for="(todo, index) in solvedTodos"
        :key="todo.id"
        :class="{ solved: todo.solved }"
      >
        Title: {{ todo.title }} {{ todo.id }} Index: {{ index }} Solved: {{ todo.solved }}
        <button id="solveTodo" @click="solveTodo(index)">-</button>
        <button id="deleteTodo" @click="deleteTodo">x</button>
      </li>
    </ul>
  </div>
</div>
</template>

<script>
export default {
  name: 'Todo',
  data () {
    return {
      todos: [
      ],

      idCounter: 0
    }
  },

  methods: {
    addNewTodo: function () {
      const todo = {}

      todo[this.idCounter] = {
        title: `new todo`,
        solved: false
      }

      this.todos.push(todo)

      this.idCounter++
    },
    deleteAllTodos: function () {
      this.todos = []
    },
    solveTodo: function (id) {
      const index = this.todos.indexOf()

      this.todos[index].solved = !this.todos[index].solved
      const todo = this.todos.splice(index, 1)
      this.todos = this.todos.concat(todo)

      console.log(this.todos)
    },
    deleteTodo: function () {
      return true
    }
  },

  computed: {
    unsolvedTodos: function () {
      return this.todos.filter(function (todo) {
        return !todo.solved
      })
    },
    solvedTodos: function () {
      return this.todos.filter(function (todo) {
        return todo.solved
      })
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#solvedTodos {
  color: red;
}

#todos .solved {
  color: red;
}
</style>
