<template>
    <h1>{{header}}</h1>
    <hr>
</template>

<script>
    export default {
        name: "VueHeader",
        props: {
            header: {
                type: String,
                required: true
            }
        }
    }
</script>

<style scoped>

</style>