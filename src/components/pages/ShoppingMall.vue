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
  </div>
</template>

<script>
  export default {
    data() {
      return {
        loctionIcon: require('../../assets/images/loction.png')
      }
    }
  }
</script>

<style scoped>
  .search-bar {
    height: 2.2rem;
    background-color: #e5017d;
    line-height: 2.2rem;
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
</style>