<template>
    <div class="card card-w70">
        <VueHeaderComponent v-if="header.length != 0" :header="header"></VueHeaderComponent>

        <div v-for="component in blogComponents" :key="component.id">
            <VueSubtitleComponent v-if="component.componentName === 'subtitle'" :subtitle="component.text"></VueSubtitleComponent>
            <VueText v-else-if="component.componentName === 'text'" :text="component.text"></VueText>
            <VueAvatarComponent v-else :avatar="component.text"></VueAvatarComponent>
        </div>

        <h3 v-if="!haveFields">Добавьте первый блок, чтобы увидеть результат</h3>
    </div>
</template>

<script>
    import VueHeaderComponent from "./ContentComponents/VueHeaderComponent";
    import VueSubtitleComponent from "./ContentComponents/VueSubtitleComponent";
    import VueText from "./ContentComponents/VueText";
    import VueAvatarComponent from "./ContentComponents/VueAvatarComponent";

    export default {
        name: "VueFormContent",
        props: {
            header: {
                type: String,
                required: true
            },
            blogComponents: {
                type: Object,
                required: true
            }
        },
        components: {VueHeaderComponent, VueSubtitleComponent, VueText, VueAvatarComponent},
        data() {
            return {
                testUrl: 'https://cdn.dribbble.com/users/5592443/screenshots/14279501/drbl_pop_r_m_rick_4x.png',
            }
        },
        computed: {
            haveFields() {
                if (this.header || (Object.getOwnPropertyNames(this.blogComponents).length  > 1)) { // other fields check too!
                    return true
                }
                return false
            }
        }
    }
</script>

<style scoped>

</style>