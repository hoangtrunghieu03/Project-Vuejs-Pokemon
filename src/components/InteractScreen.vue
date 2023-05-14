<template>
  <div class="screen">
    <div
      class="screen__inner"
      :style="{
        width: `${
          ((((920 - 16 * 4) / Math.sqrt(cardsContent.length) - 16) * 3) / 4 +
            16) *
          Math.sqrt(cardsContent.length)
        }px`,
      }"
    >
      <card-flip
        v-for="(card, index) in cardsContent"
        :key="index"
        :ref="`card-${index}`"
        :imgbackFaceUrl="`images/${card}.png`"
        :card="{ index, value: card }"
        :cardsContent="cardsContent"
        @onFlip="checkRules($event)"
      />
    </div>
  </div>
</template>

<script>
import CardFlip from "./CardFlip.vue";

export default {
  props: {
    cardsContent: {
      type: String,
    },
  },
  data() {
    return {
      rules: [],
    };
  },
  components: {
    CardFlip,
  },
  methods: {
    checkRules(card) {
      if (this.rules.length === 2) return false;
      this.rules.push(card);
      if (
        this.rules.length === 2 &&
        this.rules[0].value === this.rules[1].value
      ) {
        this.$refs[`card-${this.rules[0].index}`][0].onDisabledFlip();
        this.$refs[`card-${this.rules[1].index}`][0].onDisabledFlip();
        this.rules = [];
        const disabledElement = document.querySelectorAll(
          ".screen .card.disabled"
        );
        if (
          disabledElement &&
          disabledElement.length === this.cardsContent.length - 2
        ) {
          setTimeout(() => {
            this.$emit("onFinish");
          }, 920);
        }
      } else if (
        this.rules.length === 2 &&
        this.rules[0].value !== this.rules[1].value
      ) {
        setTimeout(() => {
          this.$refs[`card-${this.rules[0].index}`][0].onFlipBackCard();
          this.$refs[`card-${this.rules[1].index}`][0].onFlipBackCard();
          this.rules = [];
        }, 800);
      } else return false;
    },
  },
};
</script>

<style lang="css" scoped>
.screen {
  width: 100%;
  height: 100vh;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 2;
  background-color: var(--dark);
  color: var(--light);
}
.screen__inner {
  width: 424px;
  display: flex;
  flex-wrap: wrap;
  margin: 2rem auto;
}
</style>
