<template>
  <main-screen
    v-if="statusMatch === 'default'"
    @onStart="onHandleBeforeStart($event)"
  />
  <interact-screen
    v-if="statusMatch === 'match'"
    :cardsContent="setting.cardsContent"
  />
</template>

<script>
import MainScreen from "./components/MainScreen.vue";
import InteractScreen from "./components/InteractScreen.vue";
import { shuffled } from "./utils/array";

export default {
  name: "App",
  components: {
    MainScreen,
    InteractScreen,
  },
  data() {
    return {
      statusMatch: "default",
      setting: {
        totalOfBlock: 0,
        cardsContent: [],
        startedAt: null,
      },
    };
  },
  methods: {
    onHandleBeforeStart(confit) {
      this.setting.totalOfBlock = confit.totalOfBlock;
      const firstcards = Array.from(
        { length: this.setting.totalOfBlock / 2 },
        (_, i) => i + 1
      );
      const secondCards = [...firstcards];
      const card = [...firstcards, ...secondCards];
      this.setting.cardsContent = shuffled(shuffled(shuffled(card)));
      this.setting.startedAt = new Date().getTime();

      // data ready
      this.statusMatch = "match";
    },
  },
};
</script>
