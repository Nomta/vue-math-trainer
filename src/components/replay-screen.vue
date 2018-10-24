<script>
import AlertScreen from '@/components/alert-screen.vue'

export default {
    name: 'replay-screen',
    
    components: {
        AlertScreen
    },

    props: {
        options: Object
    },

    computed: {
        message() {
            return this.options.completed.task ?
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
    <alert-screen :type="options.type" :title="message" @next="next"></alert-screen>
</template>
