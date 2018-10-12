<script>
import startScreen  from '@/components/start-screen.vue'
import taskScreen   from '@/components/task-screen.vue'
import msgScreen    from '@/components/msg-screen.vue'
import finalScreen  from '@/components/final-screen.vue'

export default {
  name: 'app',

  data: () => ({
    state: 'start',
    status: '',
    level: 0,
    success: 0,
    errors: 0,
    total: 5
  }),

  components: {
    startScreen, taskScreen, msgScreen, finalScreen
  },

  computed: {
    done() {
      return this.success + this.errors === this.total
    },
    progress() {
      return {
        width: (this.success + this.errors) / this.total * 100 + '%'
      }
    }
  },

  methods: {

    getResult(status) {
      this.state = 'message'
      this.status = status ? 'success' : 'warning'

      if (status) {
        this.success++
      }
      else {
        this.errors++
      }
    },

    getTotal(status) {
      this.success = 0
      this.errors = 0
      this.state = 'start'
      if (status) 
        this.level++
    }
  }
}
</script>

<template>
  <div class="container">
    <h1>Math trainer</h1>
    <hr>
    <div class="progress">
      <div class="progress-bar bg-info" :style="progress"></div>
    </div>
    <transition name="flip" mode="out-in">
      <start-screen v-if="state === 'start'" @next="state = 'task'"/>
      <task-screen v-else-if="state === 'task'" @next="getResult" :min="10" :max="99" :len="4" :level="level"/>
      <msg-screen v-else-if="state === 'message'" @next="state = done ? 'final' : 'task'" :type="status"/>
      <final-screen v-else-if="state === 'final'" @next="getTotal" :success="success" :errors="errors"/>
      <p v-else>Неизвестная ошибка</p>
    </transition>
  </div>
</template>

<style>

.alert {
  margin: 1rem auto;
  text-align: center;
}

.buttons {
  display: flex;
  justify-content: space-between;
  margin: 2rem;
}

.container {
  padding: 1rem 0;
}

.progress-bar {
  transition: width 0.8s;
}


.flip-enter, .flip-leave-to {
  transform: rotateX(90deg);
}



.flip-enter-active, .flip-leave-active {
  transition: transform 0.3s;
}

</style>
