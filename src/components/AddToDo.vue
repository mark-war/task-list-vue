<template>
    <form @submit="addToDo">
        <input type="text" v-model="title" name="title" placeholder="Add a Task...">
        <input type="submit" value="Add Task to List" class="btn">
    </form>
</template>

<script>
export default {
    name: "AddToDo", 
    data() {
        return {
            title: ''
        }
    },
    methods: {
        addToDo(e) {
            e.preventDefault()
            const newTask = {
                id: 4,
                title: this.title,
                completed: false
            }
            this.$emit('add-todo', newTask)
            this.title = ''
        }
    }
}
</script>

<style scoped>
    form {
        display: flex;
    }
    input[type='text'] {
        flex:10;
        padding: 5px;
    }
    input[type='button'] {
        flex: 2;        
    }
</style>