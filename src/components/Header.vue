<template>
    <header>
        <h1>{{ title }}</h1>
        <Button color="green" text="Add Task" />
    </header>
</template>

<script>
import Button from './Button.vue'

export default {
        components: { Button },
        name: 'Header',
        props: { title: String }
    }
</script>

<style>
    header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 20px;
    }
</style>
