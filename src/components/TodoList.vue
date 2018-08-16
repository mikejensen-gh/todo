<template>
<div class="todo">
  <div id="todoControlsTop">
      <input v-model="newTodo" @keyup.enter="addNewTodo" placeholder="Add a new todo...">
      <v-btn id="addNewTodo" @click="addNewTodo">Add</v-btn>
      <v-btn v-if="todos.length > 0" id="deleteAllTodos" @click="deleteAllTodos" color="error">Delete all</v-btn>
  </div>

  <div id="todoList">
    <v-list v-if="todos.length > 0" two-line>
      <v-list-tile
      v-for="todo in unsolvedTodos"
      :key="todo.id"
      >
        <v-text-field class="todoTitle" v-model="todo.title" @blur="checkTodoTitle(todo.id)" solo></v-text-field>
        <v-btn class="toggleSolvedState" @click="toggleSolvedState(todo)" color="primary" outline small icon><v-icon>check</v-icon></v-btn>
        <v-btn class="deleteTodo" @click="deleteTodo(todo)" color="error" small icon><v-icon>close</v-icon></v-btn>
      </v-list-tile>
    </v-list>

    <v-divider v-if="solvedTodos.length > 0 && unsolvedTodos.length > 0"></v-divider>

    <template v-if="solvedTodos.length > 0">
      <v-list subheader two-line>
        <v-subheader>Complete</v-subheader>
        <v-list-tile
        v-for="todo in solvedTodos"
        :key="todo.id"
        >

          <v-text-field class="todoTitle solved" v-model="todo.title" @blur="checkTodoTitle(todo.id)" solo disabled></v-text-field>
          <v-btn class="toggleSolvedState" @click="toggleSolvedState(todo)" color="primary" small icon><v-icon>check</v-icon></v-btn>
          <v-btn class="deleteTodo" @click="deleteTodo(todo)" color="error" small icon><v-icon>close</v-icon></v-btn>

        </v-list-tile>
      </v-list>
    </template>
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

    toggleSolvedState: function (todo) {
      todo.solved = !todo.solved

      if (todo.solved) {
        const index = this.todos.indexOf(todo)

        this.todos.splice(index, 1)
        this.todos.push(todo)
      }
    },

    deleteTodo: function (todo) {
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
