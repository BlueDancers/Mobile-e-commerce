<template>
  <div>
    <swiper class="swiper" :options="swiperOption">
       <swiper-slide class="swiper-slide" v-for="(item, index) in slide" :key="index">
           Slide {{item}} 
        </swiper-slide>
      <div class="swiper-pagination" slot="pagination"></div>
    </swiper>
  </div>
</template>

<script>
import { swiper, swiperSlide } from "vue-awesome-swiper"
import 'swiper/dist/css/swiper.css'
  export default {
    components: {
      swiper,
      swiperSlide
    },
    data () {
      return {
        swiperOption: {
            direction:'vertical',    //vertical’设置竖排显示
            slidesPerView: 'auto',   // 设置同屏显示的数量，默认为1，这里使用auto是随意的意思。
            freeMode:true,           //默认为false，普通模式：slide滑动时只滑动一格，并自动贴合wrapper，设置为true则变为free模式，slide会根据惯性滑动可能不止一格且不会贴合。
            mousewheel:true,         //开启鼠标滚轮控制Swiper切换。可设置鼠标选项，或true使用默认值。
            pagination: {
              el: '.swiper-pagination',   //小点class
              clickable:true    //允许点击小点定位
            },
            loop:true,   //无限循环
        },
        slide: [1,2,3,4,5,6],
      }
    }
  }
</script>

<style scoped>
.swiper{
    height: 300px;
    overflow: hidden;
  }
.swiper-slide {
  height: 4rem;
}
</style>