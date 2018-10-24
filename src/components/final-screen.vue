<script>
import AlertScreen from '@/components/alert-screen.vue'
export default {
    name: 'final-screen',
    components: {
        AlertScreen
    }
}
</script>

<template>
    <alert-screen type="success" title="Поздравляем!">
        <p class="h5 mx-auto">Вы прошли все уровни!</p>
    </alert-screen>
</template>
