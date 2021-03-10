<template>
    <form class="card card-w30" @submit.prevent="submitForm">
        <div class="form-control">
            <label for="type">Тип блока</label>
            <select id="type" v-model="selected">
                <option value="title">Заголовок</option>
                <option value="subtitle">Подзаголовок</option>
                <option value="avatar">Аватар</option>
                <option value="text">Текст</option>
            </select>
        </div>

        <div class="form-control">
            <label for="value">Значение</label>
            <textarea id="value" rows="3" v-model="textarea"></textarea>
        </div>

        <button class="btn primary" :disabled="textarea.length < 3">Добавить</button>
    </form>
</template>

<script>
    export default {
        name: "VueAdminForm",
        emits: {
            changeSubtitle: null,
            changeTitle: null,
            changeText: null,
            changeAvatar: null
        },
        data() {
            return {
                selected: 'title',
                textarea: ''
            }
        },
        methods: {
            submitForm() {
                switch(this.selected) {
                    case 'title':
                        this.$emit('changeTitle', this.textarea)
                        break;
                    case 'subtitle':
                        this.$emit('changeSubtitle', this.textarea)
                        break;
                    case 'text':
                        this.$emit('changeText', this.textarea)
                        break;
                    case 'avatar':
                        this.$emit('changeAvatar', this.textarea)
                        break;
                }
                this.textarea = ''
                this.selected = 'title'
            }
        }
    }
</script>

<style scoped>

</style>