<script>
export default {
    name: 'final-screen',

    props: {
        success: Number,
        errors: Number
    },
    
    computed: {
        done() {
            return this.success * 2 > this.errors
        },
        message() {
            return this.done ? 'Следующий уровень' : 'Повторить уровень'
        }
    },

    methods: {
        next() {
            this.$emit('next', this.done)
        }
    }
}
</script>

<template>
    <div class="alert alert-info">
        <h3> Правильных ответов: {{ success }} </h3>
        <h3> Ошибок: {{ errors }} </h3>
        <button class="btn btn-info" @click="next"> {{ message }} </button>
    </div>
</template>
