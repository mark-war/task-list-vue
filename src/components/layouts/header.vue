<template>
    <header class="header">        
        <nav>
            <router-link to="/">Home</router-link> |
            <router-link to="/about">About</router-link>
        </nav>
        <h2>Task List Project</h2>
        <p>Created in Vue.JS</p>
    </header>
</template>

<script>
export default {
    name: "PageHeader"
}
</script>

<style scoped>
    .header {
        background: teal;
        color: #fff;
        text-align: center;
        padding: 10px;
    }
</style>