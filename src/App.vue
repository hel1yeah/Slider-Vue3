<template>
    <AppBg 
      v-if="sliderLength > 0"
      :bg-img="getBgImbApp"
      :name="nameAuthor"
      :status="status"
    />

  <AppSlider 
    v-if="sliderLength > 0"
    :sliderList="sliderList"
    :activeSlide="activeSlide"
    :step="step"
    :marginLength="marginLength"
  />

  <button class="slider-next" @click="next"> next </button>
  <button class="slider-prev" @click="prev"> prev </button>

</template>

<script>
import AppSlider from './components/AppSlider.vue'
import AppBg from './components/AppBg.vue'

export default {
  name: 'App',
  components: {
    AppSlider,
    AppBg,
  },
  data() {
    return {
      sliderList: [],
      activeSlide: 1,
      step: 230,
      marginLength: -230,
      status: '',
    }
  },
  computed: {
    sliderLength() {
      return this.sliderList.length
    },

    getBgImbApp(){
      return this.sliderList[this.activeSlide - 1]?.download_url
    },
    getNameAuthor(){
      return this.sliderList[this.activeSlide - 1]?.author
    }
  },
  mounted() {
    this.getSliderList()
    this.setStatus()
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
    setStatus() {
      this.status = 'open'
      setTimeout(() => {
        this.status = 'active'
      }, 3000);
    },
    next(){
      if (this.sliderLength  === this.activeSlide ) {
        return
      }
      this.activeSlide++
      this.marginLength = this.marginLength - this.step
      this.setStatus()
    },
    prev(){
      if (this.activeSlide === 1) {
        return
      }
      this.activeSlide--
      this.marginLength = this.marginLength + this.step
      this.setStatus()
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
  background-color: #2c2d2e;
  margin: 0 auto;
  overflow: hidden;
  height: 100vh;
}

</style>
