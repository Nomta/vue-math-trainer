<script>
export default {
    name: 'task-screen',

    props: {
        min: Number,
        max: Number,
        len: Number,
        level: Number
    },

    data() {
        return {
            x: this.rand(this.min, this.max),
            y: this.rand(this.min, this.max)
        }
    },

    computed: {
        answer() {
            return this.x + this.y
        },
        values() {
            const numbers = [ this.answer ]

            while(numbers.length < this.len) {
                const num = this.rand(this.answer - 10, this.answer + 10)
                if (!numbers.includes(num))
                    numbers.push(num)
            }

            return numbers.sort(() => Math.random() > 0.5)
        }
    },

    methods: {
        next(number) {
            this.$emit('next', number === this.answer)
        },

        rand(min, max) {
            return Math.floor(
                Math.random() * (max - min + 1)
            ) + min
        }
    }
}
</script>

<template>
    <div class="alert alert-secondary">
        <h3> {{ x }} + {{ y }} = ? </h3>
        <div class="buttons">
            <button class="btn btn-success px-4" 
                v-for="value in values" 
                :key="value" 
                @click="next(value)">
                    {{ value }}
            </button>
        </div>
    </div>
</template>
