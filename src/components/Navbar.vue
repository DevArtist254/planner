<template>
    <nav class="main-nav">
        <router-link :to="{ name: 'home' }">Projects</router-link>
        <router-link :to="{ name: 'AddProject' }">Add a new project</router-link>
    </nav>
</template>

<script>
export default {
    name: 'Navbar'
}
</script>

<style>
.main-nav {
    text-align: center;
    margin: 40px auto;
}

.main-nav a {
    display: block;
    text-decoration: none;
    margin: 0 10px;
    color: #999;
    font-size: 18px;
}

a.router-link-active {
    border-bottom: 2px solid #00ce89;
    padding-bottom: 4px;
}
</style>