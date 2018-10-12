<script>
export default {
    name: 'start-screen',
    methods: {
        next() {
            this.$emit('next')
        }
    }
}
</script>

<template>
    <div class="alert alert-secondary">
        <h3>Вы готовы?</h3>
        <button class="btn btn-success" @click="next">Начать</button>
    </div>
</template>
