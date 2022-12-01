<template>
    <nav class="blue-grey darken-2">
        <div class="nav-wrapper">
            <router-link to="/" class="brand-logo">Tasks</router-link>
            <ul class="right hide-on-med-and-down">
                <router-link to="/" custom v-slot="{navigate}">
                    <li><a href="#" @click="navigate" @keypress.enter="navigate" role="link">Create</a></li>
                </router-link>
                <router-link to="/list" custom v-slot="{navigate}">
                    <li><a href="#" @click="navigate" @keypress.enter="navigate" role="link">List</a></li>
                </router-link>
            </ul>
        </div>
    </nav>
</template>

<script>
export default {

}
</script>

<style scoped>
    nav {
        padding: 0 2rem;
    }
</style>