<template>
<div>
  <h1>Test</h1>
    <AddTodo @add-todo="addTodo" />
    <TodoList v-bind:todos="todos" @remove-todo="removeTodo" />
  </div>
</template>


<script>
  import AddTodo from '@/components/AddTodo';
  import TodoList from '@/components/TodoList'
  
  export default {
    name: 'App',
    data() {
      return {
        todos: []
      }
    },
    mounted() {
      fetch('https://jsonplaceholder.typicode.com/todos?_limit=10')
        .then(response => response.json())
        .then(json => this.todos=json)
    },
    methods: {
      removeTodo(id) {
        this.todos = this.todos.filter(t => t.id !== id)
      },
      addTodo(todo) {
        this.todos.push(todo)
      }
    },
    components: {
      TodoList,
      AddTodo
    }
  }
</script>
