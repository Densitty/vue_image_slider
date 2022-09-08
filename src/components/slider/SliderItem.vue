<template>
  <transition :name="transitionName">
    <div
      class="slider-item"
      v-show="slideShowing"
      @mouseenter="pauseAutoSlider"
      @mouseleave="unPauseAutoSlider"
    >
      <img :src="slide" alt="zoo image" />
    </div>
  </transition>
</template>

<script>
export default {
  emits: ["mouseEnter", "mouseLeave"],
  props: ["slide", "currentSlide", "index", "direction"],
  data: () => {
    return {};
  },
  computed: {
    slideShowing() {
      return this.currentSlide === this.index;
    },
    transitionName() {
      return this.direction === "right" ? "slide-in" : "slide-out";
    },
  },
  methods: {
    pauseAutoSlider() {
      this.$emit("mouseEnter");
    },
    unPauseAutoSlider() {
      this.$emit("mouseLeave");
    },
  },
};
</script>

<style scoped>
.slider-item {
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
}

.slider-item img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.slide-out-enter-active,
.slide-out-leave-active,
.slide-in-enter-active,
.slide-in-leave-active {
  transition: all 1s linear;
}

.slide-out-enter-from {
  transform: translateX(-100%);
}

.slide-out-leave-to {
  transform: translateX(100%);
}

.slide-in-enter-from {
  transform: translateX(100%);
}

.slide-in-leave-to {
  transform: translateX(-100%);
}
</style>
