<template>
  <div >
    <slot />
  </div>
  
</template>

<script>
export default {
  emits: ['next', 'next'],
  name:  'AppSlider',
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
// .slider {
//   width: fit-content;
//   height: 450px;
//   position: relative;
//   display: flex;
//   align-items: flex-end;
//   transition: all 1s

//   &-next, &-prev {
//     position: absolute;
//     bottom:  20px;
//   }

//   &-next {
//     left: 10px;
//   }

//   &-prev {
//     left: 80px;
//   }

// }


</style>
