<script>
import AlertScreen from '@/components/alert-screen.vue'

// 1 - 61

export default {
    name: 'task-screen',
    
    components: {
        AlertScreen
    },

    props: {
        options: Object
    },

    computed: {
        x() {
            return this.rand(this.min, this.max)
        },
        
        y() {
            return this.rand(this.min, this.max)
        },

        min() {
            return this.options.level.min
        },

        max() {
            return this.options.level.max
        },

        len() {
            return this.options.level.len
        },

        answer() {
            return this.x + this.y
        },

        values() {
            const numbers = [ this.answer ]

            while(numbers.length < this.len) {
                const randNum = this.rand(this.answer - 10, this.answer + 10)
                const num = Math.abs(randNum)
                
                if (!numbers.includes(num))
                    numbers.push(num)
            }

            return numbers.sort(() => Math.random() > 0.5)
        }
    },

    methods: {
        next(number) {
            // this.options.currentStatus = number === this.answer
            this.options.completed.task = number === this.answer
            this.$emit('next')
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
    <alert-screen :type="options.type" :title="`${ x } + ${ y } = ?`" @next="next">
            <button class="btn btn-success px-4" 
                v-for="value in values" 
                :key="value" 
                @click="next(value)">
                    {{ value }}
            </button>
    </alert-screen>

    <!-- <div class="alert alert-secondary">
        <h3> {{ x }} + {{ y }} = ? </h3>
        <div class="buttons">
            <button class="btn btn-success px-4" 
                v-for="value in values" 
                :key="value" 
                @click="next(value)">
                    {{ value }}
            </button>
        </div>
    </div> -->
</template>
