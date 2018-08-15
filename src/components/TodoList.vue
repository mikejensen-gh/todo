<template>
<div class="todo">
  <div id="todoControlsTop">
    <form>
      <input v-model="newTodo" @keyup.enter="addNewTodo" placeholder="Add a new todo...">
      <v-btn id="addNewTodo" @click="addNewTodo">Add</v-btn>
    </form>
  </div>
  <div id="todoList">
    <ul id="todos">

      <v-list
        v-for="todo in unsolvedTodos"
        :key="todo.id"
      >
        <input class="todoTitle" v-model="todo.title" @blur="checkTodoTitle(todo.id)">
        <v-btn class="toggleSolvedState" @click="toggleSolvedState(todo.id)" small>Solve</v-btn>
        <v-btn class="deleteTodo" @click="deleteTodo(todo)" color="error" small >Delete</v-btn>
      </v-list>
      
      <v-list>
        <v-list-group>
          <v-list-tile slot="activator">
            <v-list-tile-content>
              <v-list-tile-title>Solved</v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
          <v-list-tile
            v-for="todo in solvedTodos"
            :key="todo.id"
          >

            <input class="todoTitle solved" v-model="todo.title" @blur="checkTodoTitle(todo.id)">
            <v-btn class="toggleSolvedState" @click="toggleSolvedState(todo.id)" small>Unsolve</v-btn>
            <v-btn class="deleteTodo" @click="deleteTodo(todo)" color="error" small>Delete</v-btn>

          </v-list-tile>
        </v-list-group>
      </v-list>

    </ul>
  </div>
  <div id="todoControlsBottom">
    <v-btn id="deleteAllTodos" @click="deleteAllTodos" color="error">Delete all</v-btn>
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

      if (todo.solved) {
        const index = this.todos.indexOf(todo)

        this.todos.splice(index, 1)
        this.todos.push(todo)
      }
    },

    deleteTodo: function (todo) {
      // const todo = this.todos.find(obj => obj.id === id)
      const index = this.todos.indexOf(todo)

      this.todos.splice(index, 1)
    },

    checkTodoTitle: function (id) {
      const todo = this.todos.find(obj => obj.id === id)

      if (todo.title === '') {
        this.deleteTodo(todo)
      }
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
