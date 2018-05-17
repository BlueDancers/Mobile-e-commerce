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
          <img v-lazy="banner.imageUrl" width="100%">   <!-- 这里的懒加载后面写-->
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

  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      locationIcon: require('../../assets/images/location.png'),
      bannerPicArray: [
        {imageUrl:require('../../assets/images/simleVueDemoPic002.jpg')},
        {imageUrl:require('../../assets/images/simleVueDemoPic001.jpg')},
        {imageUrl:require('../../assets/images/simleVueDemoPic003.jpg')}
      ],
      category: [],
      advertest: ''
    }
  },
  created () {
    axios.get('https://www.easy-mock.com/mock/5afc389de5c64d22cc1ca565/data/data#!method=get')
    .then((data)=>{
      console.log(data.data.data.category);
      if(data.status == 200) {
        console.log(data.data.data)
        this.advertest = data.data.data.advertesPicture.PICTURE_ADDRESS
        this.category = data.data.data.category
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
  height:9rem;
}
.swiper-area {
  width: 20rem;
  clear: both;
  height: 9rem;
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
</style>
