<script>
export default {
    name: 'alert-screen',

    props: {
        title: String,
        type: String,
        options: Object
    },

    methods: {
        next() {
            this.$emit('next')
        }
    }
}
</script>

<template>
    <div class="alert" :class="`alert-${ type }`">
        <h3> {{ title }} </h3>
        <div class="buttons">
            <slot>
                <button class="btn btn-success" @click="next">Дальше</button>
            </slot>
        </div>
    </div>
</template>
