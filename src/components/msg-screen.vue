<script>
export default {
    name: 'msg-screen',

    props: {
        type: String
    },

    computed: {
        message() {
            return this.type === 'success' ?
                'Правильно!' :
                'Ошибка :('
        }
    },

    methods: {
        next() {
            this.$emit('next')
        }
    }
}
</script>

<template>
    <div class="alert" :class="`alert-${type}`">
        <h3> {{ message }} </h3>
        <button class="btn btn-success" @click="next">Дальше</button>
    </div>
</template>
