<template>
  <div class="app-bg" :style="setAppBg">
    {{bgImg}}
  </div>  
</template>

<script>
  export default {
    name: 'AppBg',
    props:{
      bgImg:{
        type: String,
        required: true,
        default: () => '',
      },
      name:{
        type: String,
        required: true,
        default: () => '',
      }
    },
    computed:{
      setAppBg(){

        return {'background' : `url(${this.bgImg})` ,
        'background-position': 'center ',
        'background-size': 'cover',
        'background-repeat': 'no-repeat',
        }

      }
    }
  }

</script>

<style lang="scss">
.app-bg {
  width: 200px;
  height: 200px;
  background-color: magenta;
  position: absolute;
  bottom: 200px;
  left: 40%;
  border-radius: 50%;
}
</style>