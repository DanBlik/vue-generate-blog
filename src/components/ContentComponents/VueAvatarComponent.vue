<template>
    <div class="avatar">
        <img :src="avatar">
    </div>
</template>

<script>
    export default {
        name: "VueAvatarComponent",
        props: {
            avatar: {
                type: String,
                required: true
            }
        }
    }
</script>

<style scoped>

</style>