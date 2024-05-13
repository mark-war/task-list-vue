<template>
    <div>
        <div v-bind:key="todo.id" v-for="todo in todos">
            <ToDoItem 
                v-bind:todo="todo" 
                v-on:toggle-complete="toggleComplete" 
                v-on:del-todo="$emit('del-todo', todo.id)" />
        </div>
    </div>
</template>

<script>

import ToDoItem from './ToDoItem.vue'

export default {
    name: 'ToDos',
    components: {
        ToDoItem
    },
    props: ["todos"],
    methods: {
        toggleComplete(todoId) {
            // Emit an event to notify the parent component of the todo ID
            this.$emit("toggle-complete", todoId);
        }
    }
}
</script>

<style scoped>

</style>