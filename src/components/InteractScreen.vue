<template>
  <div class="scre">
    <h1>Running here....</h1>
    <card-flip
      v-for="(card, index) in cardsContent"
      :key="index"
      :imgbackFaceUrl="`images/${card}.png`"
    />
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
  components: {
    CardFlip,
  },
};
</script>
