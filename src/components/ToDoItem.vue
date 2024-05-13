<template>
    <div class="todo-item" v-bind:class="{'is-completed' :todo.completed}">
        <p>
            <input type="checkbox" v-model="isChecked" @change="markComplete">
            {{ todo.title }}
            <button @click="$emit('del-todo', todo.id)" class="del">X</button>
        </p>
    </div>
</template>

<script>
export default {
    name: "ToDoItem",
    props: ["todo"],
    data() {
        return {
            isChecked: this.todo.completed
        }
    },
    methods: {
        markComplete() {
            this.$emit("toggle-complete", this.todo.id);
        },
        deleteTodo() {
            this.$emit("del-todo", this.todo.id);
        }
    }
}
</script>

<style scoped>
    .todo-item {
        background: #f4f4f4;
        padding: 10px;
        border-bottom: 1px #ccc dotted;
    }

    .is-completed {
        text-decoration: line-through;
    }

    .del {
        background: #ff0000;
        color: #fff;
        border: none;
        padding: 5px 9px;
        border-radius: 50%;
        cursor: pointer;
        float: right;
    }
</style>