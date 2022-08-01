<template>
  <MainScreen v-if="statusMatch === 'default'" v-on:onStart="onHandleBeforeStart($event)"/>
  <InteractScreen v-if="statusMatch === 'match'" :cardsContext = "settings.cardsContext" @onFinish="onGetResult"/>
  <ResultScreen v-if="statusMatch === 'result'" :timer="timer" @onStartAgain="statusMatch = 'default'"/>
  <CopyRightScreen />
</template>

<script>
import MainScreen from "./components/MainScreen.vue"
import CopyRightScreen from "./components/CopyRightScreen.vue"
import InteractScreen from "./components/InteractScreen.vue"
import ResultScreen from "./components/ResultScreen.vue"
import { shuffled } from './utils/array'
export default {
  name: 'App',
  components: {
    MainScreen,
    InteractScreen,
    CopyRightScreen,
    ResultScreen,
  },
  data() {
    return {
      settings: {
        totalOfBlocks: 0,
        cardsContext: [],
        startedAt: null,
      },
      statusMatch: "default",
      timer: 0,
    }
  },
  methods: {
    onHandleBeforeStart(configs) {
      this.settings.totalOfBlocks = configs.totalOfBlocks;
      const firstCards = Array.from(
        { length: this.settings.totalOfBlocks / 2 },
        (_, i) => i + 1
      );
      const secondCards = [...firstCards];
      const cards = [...firstCards, ...secondCards];
      this.settings.cardsContext = shuffled(shuffled(shuffled(cards)));
      this.settings.startedAt = new Date().getTime();
      this.statusMatch = "match";
    },

    onGetResult() {
      this.timer = new Date().getTime() - this.settings.startedAt;

      this.statusMatch = "result";
    }
  },
  // setup() {
  //   const onHandleBeforeStart = (config) => {
  //     console.log('config', config)
  //     this.statusMatch = "match"
  //   }

  //   return {
  //     onHandleBeforeStart
  //   }
  // }
}
</script>

<style>
</style>
