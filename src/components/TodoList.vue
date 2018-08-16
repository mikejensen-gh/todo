<template>
<div class="todo">
  <v-list>
    <v-list-tile>
      <v-text-field v-model="newTodo" @keyup.enter="addNewTodo" solo></v-text-field>
      <v-btn id="addNewTodo" @click="addNewTodo">Add</v-btn>
      <v-btn v-if="todos.length > 0" id="deleteAllTodos" @click="deleteAllTodos" color="error">Delete all</v-btn>
      <v-btn v-else disabled id="deleteAllTodos" @click="deleteAllTodo" color="error">Delete all</v-btn>
    </v-list-tile>

    <v-list-tile
      v-for="todo in unsolvedTodos"
      :key="todo.id"
    >
      <input v-model="todo.title" @blur="checkTodoTitle(todo.id)" class="w100p">
      <v-btn class="toggleSolvedState" @click="toggleSolvedState(todo)" color="primary" outline small icon><v-icon>check</v-icon></v-btn>
      <v-btn class="deleteTodo" @click="deleteTodo(todo)" color="error" small icon><v-icon>close</v-icon></v-btn>
    </v-list-tile>

    <v-divider v-if="solvedTodos.length > 0 && unsolvedTodos.length > 0"></v-divider>

    <template v-if="solvedTodos.length > 0">
      <v-subheader>Complete</v-subheader>
      <v-list-tile
        v-for="todo in solvedTodos"
        :key="todo.id"
      >
        <input v-model="todo.title" @blur="checkTodoTitle(todo.id)" class="w100p solved-todo">
        <v-btn class="toggleSolvedState" @click="toggleSolvedState(todo)" color="primary" small icon><v-icon>check</v-icon></v-btn>
        <v-btn class="deleteTodo" @click="deleteTodo(todo)" color="error" small icon><v-icon>close</v-icon></v-btn>
      </v-list-tile>
    </template>
  </v-list>
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
.solved-todo {
  font-style: italic;
  text-decoration-line: line-through;
}

.w100p {
  width: 100%;
}
</style>
