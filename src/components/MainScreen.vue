<template>
  <div class="screen">
    <h1>POKE MEMORIES</h1>
    <h3>Select mode to start game</h3>
    <button @click="onstart(16)">
      <span>4x4</span>
      <span>Easy</span>
    </button>
    <button @click="onstart(32)">
      <span>6x6</span>
      <span>Normal</span>
    </button>
    <button @click="onstart(64)">
      <span>8x8</span>
      <span>Hard</span>
    </button>
    <button @click="onstart(100)">
      <span>10x10</span>
      <span>Super Hard</span>
    </button>
  </div>
</template>

<script>
export default {
  methods: {
    onstart(totalOfBlock) {
      this.$emit("onStart", { totalOfBlock });
    },
  },
};
</script>
