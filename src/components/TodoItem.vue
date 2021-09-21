<template>
  <div :class="{ 'done': todo.done }" @click="doneTodo(todo.id)" class="todo-item">
    <p>{{todo.description}}</p>
    <button @click="deleteTodo(todo.id)"><i class="fas fa-times-circle"></i></button>
  </div>
</template>

<script>
import {EventBus} from '../eventBus';

export default {
  props: {
    'todo': {
      type: Object,
      required: true,
      default(){
        return {}
      }
    }
  },
  methods: {
    deleteTodo(todoID) {
      EventBus.$emit('deleteTodo', todoID);
    },
    doneTodo(todoID) {
      EventBus.$emit('doneTodo', todoID);
    }
  }
}
</script>

<style scoped>
  .todo-item {
    display: flex;
    justify-content: space-between;

    width: 70%;
    padding: 18px;
    background-color: rgb(80, 0, 230);
    border-radius: 5px;
    color: #fff;
    margin-bottom: 8px;

    transition: all 100ms linear;
  }

  .todo-item.done {
    background-color: rgb(0, 184, 40);
    text-decoration: line-through;
  }

  .todo-item:hover {
    -webkit-box-shadow: -1px 2px 8px 5px rgba(82,0,214,0.41); 
    box-shadow: -1px 2px 8px 5px rgba(82,0,214,0.41);
    
    cursor: pointer;
  }

  button {
    color: #fff;

    font-size: 20px;
    opacity: 0.8;

    transition: all 100ms linear;
  }

  button:hover {
    opacity: 1;
    cursor: pointer;
  }
</style>