<template>
<<<<<<< HEAD
  <div class='wraper'>
    <swiper :options="swiperOption">
    <!-- slides -->
    <swiper-slide v-for='item of swiperList' :key='item.id'>
      <img class='swiper-img' :src="item.imgUrl">
    </swiper-slide>
    <!-- Optional controls -->
    <div class="swiper-pagination"  slot="pagination"></div>
=======
  <div class='swiper'>
    <swiper  :options="swiperOption" v-if='showSwiper'> 
      <!-- slides -->
      <swiper-slide v-for="item of list" :key=item.id>
        <div class='image'>
          <img calss='swiper-image' :src='item.imgUrl'>
        </div>
      </swiper-slide>
      <!-- Optional controls -->
      <div class="swiper-pagination"  slot="pagination"></div>
>>>>>>> origin/VueBranch
    </swiper>
  </div>

</template>
<<<<<<< HEAD
<script>
export default{
  name: 'HomeSwiper',
=======

<script>
export default {
  name: 'HomeSwiper',
  props: {
    list: Array
  },
>>>>>>> origin/VueBranch
  data () {
    return {
      swiperOption: {
        pagination: '.swiper-pagination',
        loop: true
<<<<<<< HEAD
      },
      swiperList: [
        {
          id: '001',
          imgUrl: 'http://img1.qunarzz.com/p/tts4/1908/f8/7800d329239e1d02.jpg_640x360_3f8cce14.jpg'
        }, {
          id: "002",
          imgUrl: 'http://img1.qunarzz.com/p/tts1/1908/a2/979ea68b0701a402.jpg_640x360_ba644688.jpg'
        }
      ]
=======
      }
    }
  },
  computed: {
    showSwiper () {
      return this.list.length
>>>>>>> origin/VueBranch
    }
  }
}
</script>
<<<<<<< HEAD
<style lang='stylus' scoped>
   // >>>表示穿透。作用在wraper范围的所有类
  .wraper >>> .swiper-pagination-bullet-active
    background: #fff
  .wraper
    display: flex
    width: 100%
    height: 200px
    background: #eee
    .swiper-img
=======

<style lang='stylus' scoped>
  .swiper >>>.swiper-pagination-bullet-active
    background: #fff
  .swiper
    overflow: hidden
    width: 100%
    height: 0
    padding-bottom: 53.4%
    .image
      overflow: hidden
      width: 100%
      height: 0
      padding-bottom: 53.4%
    .swiper-image
>>>>>>> origin/VueBranch
      width: 100%
</style>
