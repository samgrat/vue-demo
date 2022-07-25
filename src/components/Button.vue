<template>
    <button @click="onClick()" :style="{ background : color }" class="btn">{{ text }}</button>
</template>

<script>
    export default {
        methods: {
            onClick() {
                console.log('click')
            }
        },
        name: 'Button',
        props: { color: String, text: String }
    }
</script>