<script>
export default {
    name: 'progress-bar',
    props: {
        whole: Number,
        progress: Number
    },
    computed: {
        style() {
            return {
                width: (this.progress / this.whole) * 100 + '%'
            }
        }
    }
}
</script>

<template>
    <div class="progress">
      <div class="progress-bar bg-info" :style="style"></div>
    </div>
</template>
