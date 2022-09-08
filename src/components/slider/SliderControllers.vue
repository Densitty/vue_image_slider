<template>
  <button class="slider-controls left" @click="clickPrev">Prev</button>
  <button class="slider-controls right" @click="clickNext">Next</button>
</template>

<script>
export default {
  emits: ["prevImg", "nextImg"],
  methods: {
    clickPrev() {
      this.$emit("prevImg");
    },
    clickNext() {
      this.$emit("nextImg");
    },
  },
};
</script>

<style>
.slider-controls {
  z-index: 2;
  position: absolute;
  top: calc(50% - 25px);
  border: none;
  background-color: rgba(0, 0, 0, 0.5);
  height: 50px;
  width: 100px;
  color: #fff;
  transition: 0.5s;
  cursor: pointer;
}

.slider-controls {
  background-color: rgba(0, 0, 0, 0.8);
}

.left {
  left: 0;
}

.right {
  right: 0;
}
</style>
