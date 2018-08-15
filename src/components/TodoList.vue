<template>
<div class="todo">
  <div id="todoControls">
    <button id="addTodo" v-on:click="addNewTodo">Add new todo</button>
    <button id="deleteAllTodos" @click="deleteAllTodos">Remove all todos</button>
  </div>
  <div id="todoList">
    <ul id="todos">
      <li
        v-for="(todo, index) in unsolvedTodos"
        :key="todo.id"
        :class="{ solved: todo.solved }"
      >
        Title: {{ todo.title }}
        <button class="solveTodo" @click="toggleTodoSolvedStatus(todo.id)">Solve</button>
        <button class="deleteTodo" @click="deleteTodo">Delete</button>
      </li>
      <li
        v-for="(todo, index) in solvedTodos"
        :key="todo.id"
        :class="{ solved: todo.solved }"
      >
        Title: {{ todo.title }}
        <button class="solveTodo" @click="toggleTodoSolvedStatus(todo.id)">Unsolve</button>
        <button class="deleteTodo" @click="deleteTodo">Delete</button>
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
      todos: [],
      idCounter: 0
    }
  },

  methods: {
    addNewTodo: function () {
      const todo = {
        id: [this.idCounter],
        title: 'new todo',
        solved: false
      }

      this.todos.push(todo)
      this.idCounter++
    },

    deleteAllTodos: function () {
      this.todos = []
    },

    toggleTodoSolvedStatus: function (id) {
      const todo = this.todos.find(obj => obj.id === id)
      todo.solved = !todo.solved
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
    }
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
