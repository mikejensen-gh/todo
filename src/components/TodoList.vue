<template>
<div class="todo">
  <div id="todoControlsTop">
    <form>
      <input v-model="newTodo" placeholder="Add a new Todo...">
      <v-btn id="addNewTodo" v-on:click="addNewTodo">Add</v-btn>
    </form>
  </div>
  <div id="todoList">
    <ul id="todos">
      <v-list
        v-for="todo in unsolvedTodos"
        :key="todo.id"
      >
        <span class="todoTitle">{{ todo.title }}</span>
        <v-btn small class="toggleSolvedState" @click="toggleSolvedState(todo.id)">Solve</v-btn>
        <v-btn color="error" small class="deleteTodo" @click="deleteTodo(todo.id)">Delete</v-btn>
      </v-list>
      <v-list
        v-for="todo in solvedTodos"
        :key="todo.id"
      >
        <span class="todoTitle solved">{{ todo.title }}</span>
        <v-btn small class="toggleSolvedState" @click="toggleSolvedState(todo.id)">Unsolve</v-btn>
        <v-btn color="error" small class="deleteTodo" @click="deleteTodo(todo.id)">Delete</v-btn>
      </v-list>
    </ul>
  </div>
  <div id="todoControlsBottom">
    <v-btn color="error" id="deleteAllTodos" @click="deleteAllTodos">Delete all</v-btn>
  </div>
</div>
</template>

<script>
export default {
  name: 'Todo',
  data () {
    return {
      todos: [],
      idCounter: 0,
      newTodo: ''
    }
  },

  methods: {
    addNewTodo: function () {
      const todo = {
        id: [this.idCounter],
        title: this.newTodo || 'New Todo',
        solved: false
      }

      this.todos.push(todo)
      this.idCounter++
      this.newTodo = ''
    },

    deleteAllTodos: function () {
      this.todos = []
    },

    toggleSolvedState: function (id) {
      const todo = this.todos.find(obj => obj.id === id)
      todo.solved = !todo.solved
    },

    deleteTodo: function (id) {
      const todo = this.todos.find(obj => obj.id === id)
      const index = this.todos.indexOf(todo)

      this.todos.splice(index, 1)
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
.solved {
  font-style: italic;
  text-decoration-line: line-through;
}
</style>
