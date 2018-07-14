<template>
<div class="todo">
  <div id="todoControls">
    <button id="addTodo" v-on:click="addNewTodo">Add new todo</button>
    <button id="deleteAllTodos" @click="deleteAllTodos">Remove all todos</button>
  </div>
  <div id="todoList">
    <ul id="unsolvedTodos">
      <li
        v-for="todo in unsolvedTodos"
        :key="todo.id"
      >
        {{ todo.title }}
        <button id="solveTodo" @click="solveTodo(todo.id)">-</button>
        <button id="deleteTodo" @click="deleteTodo">x</button>
      </li>
    </ul>
    <ul id="solvedTodos">
      <li
        v-for="todo in solvedTodos"
        :key="todo.id"
      >
        {{ todo.title }}
        <button id="solveTodo" @click="solveTodo(todo.id)">-</button>
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
        {
          id: 0,
          title: 'todo0',
          solved: false
        },
        {
          id: 1,
          title: 'todo1',
          solved: false
        },
        {
          id: 2,
          title: 'solvedTodo2',
          solved: true
        }
      ],

      currentId: 3
    }
  },

  methods: {
    addNewTodo: function () {
      this.todos.push({
        id: this.currentId,
        title: `new todo${this.currentId}`,
        solved: false
      })

      this.currentId++
    },
    deleteAllTodos: function () {
      this.todos = []
    },
    solveTodo: function (id) {
      this.todos[id].solved = !this.todos[id].solved;
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
</style>
