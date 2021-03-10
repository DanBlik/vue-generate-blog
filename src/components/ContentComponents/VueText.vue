<template>
    <p>{{text}}</p>
</template>

<script>
    export default {
        name: "VueText",
        props: {
            text: {
                type: String,
                required: true
            }
        }
    }
</script>

<style scoped>

</style>