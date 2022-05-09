<template>
  <div 
    class="slider" 
    :style="{ 'margin-left': `${marginLength}px` }">
    <AppSliderItem v-for="(item, index) in sliderList" 
      :key="index" 
      :activeSlide="activeSlide" 
      :myID="item.myID"
      >
      <img 
        :src="item.download_url" 
        :alt="item.author"
      >
    </AppSliderItem>
  </div>
  
</template>

<script>
import AppSliderItem from "./AppSliderItem.vue"

export default {
  emits: ['next', 'next'],
  name:  'AppSlider',
  components: {
    AppSliderItem,
  },
  props:{
    sliderList: {
      type: Array,
      required: true,
      default: () => []
    },
    activeSlide: {
      type: Number,
      required: true,
      default: () => 1
    },
    step: {
      type: Number,
      required: true,
      default: () => 230
    },
    marginLength: {
      type: Number,
      required: true,
      default: () => -230
    }
  }
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
.slider {
  width: fit-content;
  height: 450px;
  position: absolute;
  display: flex;
  align-items: flex-end;
  transition: margin-left 1s ease-in-out;
  bottom: 50px;
  left: 60%;

  &-next, &-prev {
    position: absolute;
    bottom:  20px;
  }

  &-next {
    left: 10px;
  }

  &-prev {
    left: 80px;
  }
}
</style>
