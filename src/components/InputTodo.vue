<template>
  <div class="input-todo">
    <input type="text" v-model="newTodo.description" placeholder="Digite aqui a descrição da sua tarefa">
    <button @click="addTodo">+</button>
  </div>
</template>

<script>
export default {
  data(){
    return {
      newTodo: {
        'description': '',
        'done': false
      }
    }
  },
  methods: {
    addTodo(){
      if(this.newTodo.description){
        const newTodoDescription = this.newTodo.description;
        this.$emit('addTodo', newTodoDescription);
      }
    }
  }
}
</script>

<style scoped>
  .input-todo {
    display: flex;
    justify-content: center;
    margin: 16px 0;;
  }

  input[type='text'] {
    padding: 8px 16px;
    border: 0.5px solid rgb(80, 80, 80);
    width: 80%;
    font-size: 16px;
    border-top-left-radius: 5px;
    border-bottom-left-radius: 5px;
  }

  input[type='text']:active, input[type='text']:focus {
    border-color: rgb(22, 22, 22);
  }

  button {
    width: 20%;
    padding: 4px;
    text-align: center;
    background-color: rgb(19, 161, 0);
    color: #fff;
    font-size: 22px;

    border-top-right-radius: 5px;
    border-bottom-right-radius: 5px;
  }

  button:hover {
    cursor: pointer;
  }
  
</style>