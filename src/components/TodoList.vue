<template>
    <div class="todos-list">
        <TodoItem v-for="todo in todos" :todo="todo" :key="todo.description"/>
    </div>
</template>

<script>
import TodoItem from '@/components/TodoItem.vue';

export default {
    components: {TodoItem},
    props: {
        'todos': {
            type: Array,
            required: true,
            default() {
                return []
            }
        }
    }
}
</script>

<style scoped>
    .todos-list {
        display: flex;
        flex-direction: column;
        align-items: center;
    }
</style>