<template>
  <div id="app">
    <div class="section">
      <div class="container">
        <TodoItem :todos="todos" @addTodo="addTodo" @onComplete="completed" @onDelete="deletetodo" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import "bulma/css/bulma.css";
import TodoItem from './components/TodoItem.vue'
export default {
  name: 'App',
  components: {
    TodoItem,
  },
  data() {
    return {
      // todos: [
      //   {
      //     "userId": 1,
      //     "id": 1,
      //     "title": "delectus aut autem",
      //     "completed": false
      //   },
      //   {
      //     "userId": 1,
      //     "id": 2,
      //     "title": "quis ut nam facilis et officia qui",
      //     "completed": false
      //   },
      //   {
      //     "userId": 1,
      //     "id": 3,
      //     "title": "fugiat veniam minus",
      //     "completed": false
      //   },
      //   {
      //     "userId": 1,
      //     "id": 4,
      //     "title": "et porro tempora",
      //     "completed": true
      //   },
      //   {
      //     "userId": 1,
      //     "id": 5,
      //     "title": "laboriosam mollitia et enim quasi adipisci quia provident illum",
      //     "completed": false
      //   },
      // ]

      todos:null
    }
  },
  methods: {
    addTodo(todo) {
      this.todos.unshift(todo)
    },
    deletetodo(id) {
       let deleted_todos = this.todos.filter(todo => todo.id != id);
      // this.todos.splice(id, 1);
       this.todos = deleted_todos;
    },
    completed(id) {
      const updated_todos = this.todos.map(todo => todo.id == id ? Object.assign(todo, { completed: true }) : todo);
      this.todos = updated_todos;
    },
  },
  mounted() {
    axios.get('https://jsonplaceholder.typicode.com/posts/1/comments')
      .then(response => ( this.todos  = response.data) )
    }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
