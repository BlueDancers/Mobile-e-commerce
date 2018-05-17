<template>
  <div>
    <div class="search-bar">
      <van-row class="test-row">
      <!-- vant是24布局 -->
        <van-col span="3">
          <img :src="locationIcon" alt="" width="50%" class="localtion-icon">
          </van-col>
        <van-col span="16">
          <input type="text" class="search-input" placeholder="查找">
        </van-col>
        <van-col span="5">
            <van-button size="mini">查看</van-button>
        </van-col>
     </van-row>
    </div>
    <div class="swiper-area">
      <van-swipe :autoplay="2000" class="van-swipe">
        <van-swipe-item v-for="(banner,index) in bannerPicArray" :key="index">
          <img v-lazy="banner.image" width="100%">   <!-- 这里的懒加载后面写-->
        </van-swipe-item>
      </van-swipe>
    </div>
    <div class="type-bar">
      <div  v-for="(cate,index) in category" :key="index" >
          <img v-lazy="cate.image" width="90%" />
          <span>{{cate.mallCategoryName}}</span> 
      </div>
    </div>
    <div class="ad-adver">
      <img v-lazy="advertest" width="100%">
    </div>
    <div class="recommend-list">
      <div class="recommend-title">
        商品推荐
      </div>
      <div class="recommend-body">
        <swiper :options="swiperOption">
          <swiper-slide v-for="(item,index) in recommendGoods" :key="index">
            <div class="recommed-item">
              <img :src="item.image" width="80%">
              <div>{{item.goodName}}</div>
              <div>${{item.price}} (${{item.mallPrice}})</div>
            </div>
          </swiper-slide>
        </swiper>
      </div>
    </div>
    <!-- <swiperdefault></swiperdefault> 关于比较多的vue-awesome-swiper api在这里面 -->
  </div>
</template>

<script>
import axios from 'axios'
import 'swiper/dist/css/swiper.css'
import swiperdefault from '../swiper/swiperDefault'
import { swiper, swiperSlide } from "vue-awesome-swiper";
export default {
  components: {
    swiper,
    swiperSlide,
    swiperdefault
  },
  data() {
    return {
      locationIcon: require('../../assets/images/location.png'),
      bannerPicArray: [],
      category: [],
      advertest: '',
      recommendGoods: '',
      floor1: [],
      swiperOption: {
        slidesPerView:3,
        loop:true,     //无限滚动
         pagination: {
            el: '.swiper-pagination',
            clickable:true
        }
      }
    }
  },
  created () {
    axios.get('https://www.easy-mock.com/mock/5afc389de5c64d22cc1ca565/data/data#!method=get')
    .then((data)=>{
      if(data.status == 200) {
        console.log(data.data.data)
        this.advertest = data.data.data.advertesPicture.PICTURE_ADDRESS
        this.category = data.data.data.category
        this.bannerPicArray = data.data.data.slides
        this.recommendGoods = data.data.data.recommend
        this.floor1 = data.data.data.floor1
      }
    })
    .catch(()=> {
      console.log("失败");
    })
  }
}
</script>

<style scoped>
.test-row {
  text-align: center;
}
.search-bar {
  height: 2.2rem;
  background-color: #e5017d;
  line-height: 2.2rem;
}
.search-input {
  width: 100%;
  height:1.3rem ;
  border: 0px;
  border-bottom: 1px solid #f2f2f2 !important;
  background-color: #e5017d;
  color: white;
  font-size: 0.8rem;
}
.localtion-icon {
  width: 60%;
  position: relative;
  top: 0.4rem;
}
.van-swipe {
  height:8rem;
}
.swiper-area {
  width: 20rem;
  clear: both;
  height: 8rem;
}
.type-bar{
  background-color: #fff;
  margin:0 .3rem .3rem .3rem;
  font-size:14px;
  display: flex;
  justify-content: space-around;
}
.type-bar div{
  padding: .3rem;
  font-size: 12px;
  text-align: center;
}
.recommend-list {
  background: #fff;
  margin-top: 0.3rem
}
.recommend-title {
  border: 1px solid #eee;
  text-align: left;
  font-size: 14px;
  padding: .2rem;
  color: #e5017d;
}
.recommed-item {
  width:100%;
  border-right: 1px solid #eee;
  font-size: 12px;
  text-align: center;
}
</style>
