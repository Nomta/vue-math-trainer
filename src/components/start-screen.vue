<script>
import AlertScreen from '@/components/alert-screen.vue'
export default {
    name: 'start-screen',

    props: {
        options: Object
    },

    components: {
        AlertScreen
    },
    methods: {
        next() {
            this.$emit('next')
        }
    }
}
</script>

<template>
    <alert-screen :type="options.type" title="Вы готовы?" @next="next"></alert-screen>
    <!-- <div class="alert alert-primary">
        <h3>Вы готовы?</h3>
        <button class="btn btn-success" @click="next">Начать</button>
    </div> -->
</template>
