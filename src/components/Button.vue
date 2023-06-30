<template>
    <button @click="handleClick" :style="{background: background}">
        {{ buttonText }}
    </button>
</template>


<script>
    export default {
       props: {
        buttonText: {
            type: String,
            required: true
        },
        background: {
            type: String,
            required: true
        }
       },
       methods: {
        handleClick() {
            this.$emit('button-click');
        },
        }
    }
</script>