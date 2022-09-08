<template>
  <div class="slide_indicators">
    <button
      class="indicator"
      :class="{ active: active === idx }"
      v-for="(btn, idx) in count"
      :key="idx"
      @click="changeImg(idx)"
    ></button>
  </div>
</template>

<script>
export default {
  props: ["count", "active"],
  props: {
    count: { type: Number, required: true },
    active: { type: Number, required: true },
  },
  emits: ["switch"],
  methods: {
    changeImg(index) {
      this.$emit("switch", index);
    },
  },
};
</script>

<style scoped>
.slide_indicators {
  position: absolute;
  bottom: 0.8rem;
  z-index: 3;
  display: flex;
  justify-content: center;
  width: 100%;
}

.indicator {
  height: 20px;
  width: 20px;
  border-radius: 50%;
  background-color: rgba(255, 255, 255, 0.5);
  border: none;
  display: inline-block;
  margin-right: 0.4rem;
  cursor: pointer;
  transition: all 500ms;
}

.indicator:hover,
.indicator.active {
  background-color: rgba(255, 255, 255, 1);
}
</style>
