<template>
  <div>
    <div class="search-bar">
      <van-row>
        <van-col span="3">
          <img :src="loctionIcon" alt="" width="80%" class="localtion-icon">
        </van-col>
        <van-col span="16">
          <input type="text" class="search-input">
        </van-col>
        <van-col span="5">
          <van-button size="mini">查找</van-button>
        </van-col>
      </van-row>
    </div>
    <!-- swiper area -->
    <div class="swiper-area">
      <van-swipe :autoplay="3000">
        <van-swipe-item v-for="(banner,index) in bannerPicArray" :key="index">
          <img v-lazy="banner.image" width="100%">
        </van-swipe-item>
      </van-swipe>
    </div>
    <!-- type bar -->
    <div class="type-bar">
      <div v-for="(cate, index) in category" :key="index">
        <img v-lazy="cate.image" width="100%">
        <span>{{cate.mallCategoryName}}</span>
      </div>
    </div>
    <!-- Ad banner area -->
    <div class="ad-banner">
      <img v-lazy="adBanner.PICTURE_ADDRESS" width="100%">
    </div>
    <!-- 商品推荐 -->
    <div class="recommend-area">
      <div class="recommend-title">
        商品推荐
      </div>
      <div class="recommend-body">
        <swiper :options="swiperOption">
          <swiper-slide v-for="(item, index) in reCommendGoods" :key="index">
            <div class="recommend-item">
              <img :src="item.image" width="80%">
              <div>{{item.goodsName}}</div>
              <div>￥{{item.price}}(￥{{item.mallPrice}})</div>
            </div>
          </swiper-slide>
        </swiper>
      </div>
    </div>
    <!-- floor -->
    <div class="floor">
      <div class="floor-anomaly">
        <div class="floor-one">
          <img :src="floor1_0.image" width="100%">
        </div>
        <div class="floor-two">
          <div>
            <img :src="floor1_1.image" width="100%">
          </div>
          <div>
            <img :src="floor1_2.image" width="100%">
          </div>
        </div>       
      </div>
      <div class="floor-rule">
        <div v-for="(item ,index) in floor1.slice(3)" :key="index">
          <img :src="item.image" width="100%"/>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import {swiper, swiperSlide} from "vue-awesome-swiper"
import 'swiper/dist/css/swiper.css'
  export default {
    data() {
      return {
        loctionIcon: require('../../assets/images/loction.png'),
        bannerPicArray: [],
        category: [],
        adBanner: '',
        // 推荐
        reCommendGoods: [],
        swiperOption: {
          slidesPerView: 3
        },
        floor1: [],
        floor1_0: {},
        floor1_1: {},
        floor1_2: {},
      }
    },
    components: {
      swiper,
      swiperSlide
    },
    created () {
      axios({
        url: 'https://www.easy-mock.com/mock/5af1c23c681e1812f5771eea/vanmall/index',
        method: 'get'
      }).then(resp => {
        if (resp.status === 200) {
          this.category = resp.data.data.category
          this.adBanner = resp.data.data.advertesPicture //获得广告图片
          this.bannerPicArray = resp.data.data.slides   //轮播图片
          this.reCommendGoods = resp.data.data.recommend //推荐商品
          this.floor1 = resp.data.data.floor1
          this.floor1_0 =this.floor1[0]
          this.floor1_1 = this.floor1[1]
          this.floor1_2 = this.floor1[2]
        }
      }).catch(error => {
        console.log(error)
      })
    }
  }
</script>

<style scoped>
  .search-bar {
    height: 2.2rem;
    background-color: #e5017d;
    line-height: 2.2rem;
    overflow: hidden;
  }
  .search-input{
    width: 100%;
    height: 1.3rem;
    border-top: 0px;
    border-left: 0px;
    border-right: 0px;
    border-bottom: 1px solid #fff !important;
    background-color: #e5017d;
    color: #fff;
  }
  .localtion-icon{
    padding-top:.2rem;
    padding-left: .3rem;
  }
  .swiper-area{
    clear: both;
    max-height: 10rem;
    overflow: hidden;
  }
  .type-bar{
    /* 背景色 */
    background-color: #fff;
    /* 外边距 */
    margin: 0 .3rem .3rem .3rem;
    /* 圆角 */
    border-radius: .3rem;
    /* 字体 */
    font-size: 14px;
    display: flex;
    /* 横向布局 */
    flex-direction: row;
    /* 不换行 */
    flex-wrap: nowrap;
  }
  .type-bar div{
    padding:  .3rem;
    font-size: 12px;
    text-align: center;
  }
  .recommend-area{
    background-color: #fff;
    margin-top: .3rem;
  }
  .recommend-title{
    border-bottom: 1px solid #eee;
    font-size: 14px;
    padding: .2rem;
    color: #e5017d;
  }
  .recommend-body{
    border-bottom: 1px solid #eee;
  }
  .recommend-item{
    width: 99%;
    border-right: 1px solid #eee;
    font-size: 12px;
    text-align: center;
  }
  .floor-anomaly{
    display: flex;
    flex-direction:row;
    background-color: #fff;
    border-bottom: 1px solid #ddd; 
  }
  .floor-anomaly div{
    width: 10rem;
    box-sizing: border-box;
    -webkit-box-sizing: border-box;
  }
  .floor-one{
    border-right: 1px solid #ddd;
  }
  .floor-two{
    border-bottom: 1px solid #ddd;
  }
  .floor-rule{
      display: flex;
      flex-direction: row;
      /* 自动换行 */
      flex-wrap:wrap;
      background-color: #fff;
 
  }
  .floor-rule div{
      -webkit-box-sizing: border-box;
      box-sizing: border-box;
      width:10rem;
      border-bottom:1px solid #ddd;
  }
  .floor-rule div:nth-child(odd){
      border-right: 1px solid #ddd;
  }
</style>