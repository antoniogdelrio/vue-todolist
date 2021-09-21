<template>
  <main>
    <h1>Todo List App</h1>
    <ProgressBar :todosLength="todosLength" :doneTodosLength="doneTodosLength"/>
    <InputTodo @addTodo="addTodo" />
    <TodoList :todos="todos" />
  </main>
</template>

<script>
import ProgressBar from './components/ProgressBar.vue';
import InputTodo from './components/InputTodo.vue';
import TodoList from './components/TodoList.vue';
import {EventBus} from './eventBus';

export default {
  components: {
    ProgressBar,
    InputTodo,
    TodoList 
  },
  data(){
    return {
      todos: []
    }
  },
  methods: {
    addTodo(newTodoDescription){
      const equalTodos = this.todos.filter((todo) => {
        return todo.description == newTodoDescription
      })

      if(equalTodos.length > 0)
        return;

      this.todos.push({
        'id': Math.floor((1 + Math.random()) * 0x10000).toString(16).substring(1),
        'description': newTodoDescription,
        'done': false
      })
    }
  },
  created(){
    EventBus.$on('deleteTodo', (id) => {
      this.todos = this.todos.filter((todo) => {
        return todo.id != id;
      })
    })

    EventBus.$on('doneTodo', (id) => {
      this.todos = this.todos.map((todo) => {
        return {
          ...todo,
          'done': todo.id == id ? !todo.done : todo.done
        }
      })
    })

    if(localStorage.getItem('todos')){
      const savedTodos = JSON.parse(localStorage.getItem('todos'));
      this.todos = savedTodos;
    }
  },
  computed: {
    todosLength(){
      return this.todos.length;
    },
    doneTodosLength(){
      return this.todos.filter((todo) => {
        return todo.done;
      }).length
    }
  },
  watch: {
    todos(todosData){
      if(localStorage.getItem('todos')){
        return localStorage.setItem('todos', JSON.stringify(todosData));
      }
      localStorage.setItem('todos', JSON.stringify([]));
    }
  }
}
</script>

<style scoped>
  h1 {
    text-align: center;
    margin-bottom: 24px;
  }

  main {
    max-width: 70%;
    margin: 0 auto;
  }
</style>