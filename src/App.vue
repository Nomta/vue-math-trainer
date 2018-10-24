<script>
import StartScreen  from '@/components/start-screen.vue'
import TaskScreen   from '@/components/task-screen.vue'
import ReplayScreen from '@/components/replay-screen.vue'
import ResultScreen from '@/components/result-screen.vue'
import FinalScreen  from '@/components/final-screen.vue'
import ProgressBar  from '@/components/progress-bar.vue'

import { State, Levels } from '@/state'

export default {
  name: 'app',

  data: () => ({
    currentComponent: StartScreen,
    state: State,
    levels: Levels,
    levelIndex: 0,
    tasksPerLevel: 5
  }),

  components: {
    StartScreen, TaskScreen, ReplayScreen, ResultScreen, FinalScreen, ProgressBar
  },

  computed: {
    levelIsDone() {
      return this.tasksCount === this.tasksPerLevel
    },

    tasksCount() {
      return this.state.results.success + this.state.results.errors
    },

    levelsLength() {
      return this.levels.length
    }
  },

  methods: {

    toggleComponent() {
      switch(this.currentComponent) {
        case StartScreen:
          this.linkToTask()
          break
        case TaskScreen:
          this.linkToReplay()
          break
        case ReplayScreen:
          this.linkToResult()
          break
        case ResultScreen:
          this.linkToFinal()
          break
        //default: break
      }
    },

    linkToTask() {
      if (this.levelIndex + 1 === this.levelsLength)  
        this.state.nextLevel = false
      this.currentComponent = TaskScreen
    },

    linkToReplay() {
      if (this.state.completed.task) { 
        this.state.results.success++
        this.state.type = 'success'
      }
      else {
        this.state.results.errors++
        this.state.type = 'warning'
      }
      this.currentComponent = ReplayScreen
    },

    linkToResult() {
      this.state.type = 'secondary'
      this.currentComponent = this.levelIsDone ? ResultScreen : TaskScreen
    },

    linkToFinal() {
      if (this.state.completed.app) {
        this.currentComponent = FinalScreen
        return
      }

      this.state.results = {
        success: 0,
        errors: 0
      }
      
      if (this.state.nextLevel && this.state.completed.level) 
        this.state.level = this.levels[++this.levelIndex]
    
      this.state.completed.level = false
      this.currentComponent = StartScreen
    },
  }
}
</script>

<template>
  <div class="container">
    <h1>Math trainer</h1>
    <h3> Уровень {{ levelIndex + 1 }} </h3>
    <hr>
    <progress-bar :progress="tasksCount" :whole="tasksPerLevel"></progress-bar>
    <transition name="flip" mode="out-in">
      <component :is="currentComponent" :options="state" @next="toggleComponent"></component>
    </transition>
  </div>
</template>
