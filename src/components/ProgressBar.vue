<template>
  <div class="progress-bar">
    <div class="progress-bar-completed" :style="{'width': percentage + '%'}"></div>
    <div class="progress-bar-percentage">
      <p>Progresso: {{percentage}}%</p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    'todosLength': {
      type: Number,
      required: true
    },
    'doneTodosLength': {
      type: Number,
      required: true
    }
  },
  computed: {
    percentage(){
      if(this.todosLength)
        return (this.doneTodosLength/this.todosLength)*100;
      
      return 0;
    }
  }
}
</script>

<style>
  .progress-bar {
    width: 80%;
    height: 30px;
    border-radius: 8px;
    border: 1px solid #000;
    background-color: #fff;
    margin: 0 auto;
  }

  .progress-bar-completed {
    height: 28px;
    border-radius: 8px;
    background-color: rgb(0, 184, 40);
  }

  .progress-bar-percentage {
    position: relative;
    bottom: 28px;

    display: flex;
    align-items: center;
    justify-content: center;
    
    width: 100%;
    height: 30px;
    text-align: center;
    color: rgb(189, 189, 189);
  }
</style>