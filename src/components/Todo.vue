<template>
  <div class="todo">
    <div id="todoControls">
      <button id="addTodo" v-on:click="addNewTodo">Add new todo</button>
      <button id="removeAllTodos" v-on:click="removeAllTodos">Remove all todos</button>
    </div>
    <div id="todoList">
      <ul>
        <li v-for="todo in todos">
          {{ todo.title }}
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
            title: "todo 1"
          },
          {
            title: "todo 2"
          }
        ]
      }
    },
    methods: {
      addNewTodo: function() {
        this.todos.push({title: 'new todo'})
      },
      removeAllTodos: function() {
        this.todos = []
      }
    },

    computed: {

    }

  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
