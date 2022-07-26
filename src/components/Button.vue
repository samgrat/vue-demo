<template>
    <button @click="onClick()" :style="{ background : color }" class="btn">{{ text }}</button>
</template>

<script>
    export default {
        methods: {
            onClick() {
                this.$emit('btn-click')
            }
        },
        name: 'Button',
        props: { color: String, text: String }
    }
</script>