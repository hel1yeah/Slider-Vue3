<template>
  <AppSlider
    class="slider"
    :style="{ 'margin-left': `${marginLength}px` }"
  >
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
    

  </AppSlider>
  <button class="slider-next" @click="next"> next </button>
  <button class="slider-prev" @click="prev"> prev </button>
</template>

<script>
import AppSlider from './components/AppSlider.vue'
import AppSliderItem from './components/AppSliderItem.vue'

export default {
  name: 'App',
  components: {
    AppSlider,
    AppSliderItem,
  },
  data() {
    return {
      sliderList: [],
      activeSlide: 1,
      step: 230,
      marginLength: -230,
    }
  },
  computed: {
    sliderLength() {
      return this.sliderList.length
    },

  },
  mounted() {
    this.getSliderList()
  },
  methods: {
    getSliderList() {
      fetch('https://picsum.photos/v2/list?page=3&limit=10')
        .then((response) => {
          return response.json();
        })
        .then((data) => {
          this.setSliderListMyid(data)
        }).catch(err => {
          console.log(err);
        })
    },
    setSliderListMyid(data) {
      const tets = []
      for (let i = 0; i < data.length; i++) {
        tets.push({
          ...data[i],
          myID: i
        })
      }
      this.sliderList = tets
    },
    next(){
      if (this.sliderLength  === this.activeSlide ) {
        return
      }
      this.activeSlide++
      this.marginLength = this.marginLength - this.step
    },
    prev(){
      if (this.activeSlide === 1) {
        return
      }
      this.activeSlide--
      this.marginLength = this.marginLength + this.step
    }
  }

}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  position: relative;
  color: #2c3e50;
  margin: 0 auto;
  overflow: hidden;
  height: 100vh;
}
.slider {
  width: fit-content;
  height: 450px;
  position: relative;
  display: flex;
  align-items: flex-end;
  transition: margin-left 1s ease-in-out;;

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
