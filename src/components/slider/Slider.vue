<template>
  <div class="slider">
    <div class="slider-inner" :style="dimension">
      <slide-indicators
        :count="slides.length"
        :active="current"
        @switch="switchSlide"
        v-if="indicators"
      ></slide-indicators>

      <slider-item
        :slide="slide"
        v-for="(slide, index) in slides"
        :key="index"
        :currentSlide="current"
        :index="index"
        :direction="direction"
        @mouse-enter="stopSlideTimer"
        @mouse-leave="startSlideTimer"
      ></slider-item>

      <slider-controllers
        @prevImg="cyclePrev"
        @nextImg="cycleNext"
        v-if="controls"
      ></slider-controllers>
    </div>
  </div>
</template>

<script>
import SliderItem from "./SliderItem.vue";
import SliderControllers from "./SliderControllers.vue";
import SlideIndicators from "./SlideIndicators.vue";

export default {
  components: {
    SliderItem,
    SliderControllers,
    SlideIndicators,
  },
  props: {
    controls: { type: Boolean, default: false },
    indicators: { type: Boolean, default: false },
    interval: { type: Number, default: 5000 },
    width: { type: Number, default: 1000 },
    height: { type: Number, default: 400 },
  },
  data() {
    return {
      slides: [
        "./assets/image1.jpg",
        "./assets/image2.jpg",
        "./assets/image3.jpg",
        "./assets/image4.jpg",
        "./assets/image5.jpg",
        "./assets/image6.jpg",
      ],
      current: 0,
      slideStart: null,
      direction: "right",
    };
  },
  computed: {
    dimension() {
      return {
        width: `${this.width ? `${this.width}px` : "80vw"}`,
        height: `${this.height}px`,
      };
    },
  },
  methods: {
    setCurrentSlide(index) {
      this.current = index;
    },
    cyclePrev(step = -1) {
      const index =
        this.current < 1 ? this.slides.length - 1 : this.current + step;

      this.setCurrentSlide(index);
      this.direction = "left";
      // restart auto-slider on click of prev btn
      this.startSlideTimer();
    },
    next(step = 1) {
      const index =
        this.current >= this.slides.length - 1 ? 0 : this.current + step;

      this.setCurrentSlide(index);
      this.direction = "right";
    },
    cycleNext(step = 1) {
      this.next(step);
      // restart auto-slider on click of next btn
      this.startSlideTimer();
    },
    startSlideTimer() {
      this.stopSlideTimer();

      this.slideStart = setInterval(() => {
        this.next();
      }, this.interval);
    },
    stopSlideTimer() {
      clearInterval(this.slideStart);
    },
    switchSlide(index) {
      /* first calculate the step to move; if there are 6 images and the current image showing is 1, then clicking on image 6 btn will cycle through 5 images forward to get to the 6th img (5 imgs backwards for reverse case) */
      let stepToMove = index - this.current;

      if (stepToMove > 0) {
        this.cycleNext(stepToMove);
      } else {
        this.cyclePrev(stepToMove);
      }
    },
  },
  mounted() {
    this.startSlideTimer();
  },
  beforeUnmount() {
    this.stopSlideTimer();
  },
};
</script>

<style scoped>
.slider {
  display: flex;
  justify-content: center;
}

.slider-inner {
  position: relative;
  /* width: 70vw;
  height: 400px; */
  overflow: hidden;
}
</style>
