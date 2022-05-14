<template>
  <main-screen v-if="statusMatch === 'default'" @onStart="onHandleBeforeStart($event)"></main-screen>
  <interact-screen v-if="statusMatch === 'match'" :cardsContent="setting.cardsContent" @onFinish="onGetResult"></interact-screen>
  <result-screen v-if="statusMatch === 'result'" :timer="timer" @onStartAgain="statusMatch = 'default'"></result-screen>
</template>

<script>
import MainScreen from './components/MainScreen.vue'
import InteractScreen from './components/InteractScreen.vue'
import {shuffled} from './utils/array.js'
import ResultScreen from './components/ResultScreen.vue'

export default {
  name: 'App',
  components: {
    MainScreen,
    InteractScreen,
    ResultScreen
  },
  data() {
    return {
      setting: {
        totalOfBlocks: 0,
        cardsContent: [],
        startedAt: null
      },
      statusMatch: 'default',
      timer: 0,
    }
  },
  methods: {
    onHandleBeforeStart(config) {
      this.setting.totalOfBlocks = config.totalOfBlocks;
       
      const firstCards = Array.from({ length: this.setting.totalOfBlocks /2 }, (e,i) =>i+1);
      const secondCards = [...firstCards];
      const cards = [...firstCards, ...secondCards];
      this.setting.cardsContent = shuffled(shuffled(shuffled(shuffled(cards))));

      this.setting.startedAt = new Date().getTime();

      this.statusMatch = 'match'
    },
    onGetResult() {
      this.timer = new Date().getTime() - this.setting.startedAt;
      this.statusMatch = 'result'
      
    }
  }
}
</script>


