<template>
  <div :class="['slider__item', {'slider__item-active' : activeSlide === myID}, {'slider__item-none' : myID < activeSlide}]">
    <slot />
  </div>
</template>

<script>


export default {
  name: 'AppSliderItem',
  props: {
    activeSlide: {
      type: Number,
      required: true,
      default: () => 0
    },
    myID: {
      type: Number,
      required: true,
      default: () => 0
    }
  },
  setup() {
    return {}
  }
}
</script>

<style lang="scss">
.slider__item {
  width: 190px;
  height: 380px;
  margin: 0 40px 0 0;
  overflow: hidden;
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: 1s;
  &-active {
    height: 420px;
    width: 220px;
  }
  &-none {
    opacity: 0;
  }
  & img {
    height: 100%
  }
}
</style>