<script>
import AlertScreen from '@/components/alert-screen.vue'

export default {
    name: 'result-screen',

    components: {
        AlertScreen
    },

    props: {
        options: Object
    },
    
    computed: {
        completed() {
            return this.success > this.errors * 2
        },
        success() {
            return this.options.results.success
        },
        errors() {
            return this.options.results.errors
        }
    },

    methods: {
        next() {
            this.options.completed.level = this.completed
            this.$emit('next')
        },
        repeat() {
            this.$emit('next')
        },
        finish() {
            this.options.completed.app = true
            this.$emit('next')
        }
    }
}
</script>

<template>
    <alert-screen :type="options.type" :title="`Правильных ответов: ${ success } Ошибок: ${ errors }`" @next="next">
        <button class="btn btn-secondary" @click="repeat">Повторить уровень</button>
        <button class="btn btn-success" :disabled="!completed" @click="next" v-if="options.nextLevel">Следующий уровень</button>
        <button class="btn btn-success" :disabled="!completed" @click="finish" v-else>Завершить тренировку</button>
    </alert-screen>
</template>
