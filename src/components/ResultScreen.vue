<template>
  <h1>bạn đã thành công</h1>
  <p>{{ Math.round(timer / 1000) }}</p>
  <button @click="onStargame()">Start game</button>
</template>

<script>
export default {
  props: {
    timer: {
      type: Number,
      required: true,
    },
  },
  methods: {
    onStargame() {
      this.$emit("onStarGame");
    },
  },
};
</script>
