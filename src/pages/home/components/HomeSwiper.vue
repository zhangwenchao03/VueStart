<template>
  <div class='swiper'>
    <swiper  :options="swiperOption" >
      <!-- slides -->
      <swiper-slide v-for="item of swiperList" :key=item.id>
        <div class='image'>
          <img calss='swiper-image' :src='item.imgUrl'>
        </div>
      </swiper-slide>
      <!-- Optional controls -->
      <div class="swiper-pagination"  slot="pagination"></div>
    </swiper>
  </div>

</template>

<script>
export default {
  name: 'HomeSwiper',
  data () {
    return {
      swiperOption: {
        pagination: '.swiper-pagination',
        loop: true
      },
      swiperList: [{
        id: '001',
        imgUrl: 'https://tr-osdcp.qunarzz.com/tr-osd-tr-manager/img/3afcd3ace835ef3d0574be8f1f2f63c9.jpg_r_640x290x70_fa4ea15c.jpg'
      },
      {
        id: '002',
        imgUrl: 'https://tr-osdcp.qunarzz.com/tr-osd-tr-manager/img/9222dc2064de6ab9b122272c5200f1af.jpg_r_640x290x70_73682f61.jpg'
      },
      {
        id: '003',
        imgUrl: 'https://tr-osdcp.qunarzz.com/tr-osd-tr-manager/img/fc095bd09000b60b89c45b508be0734e.jpg_r_640x290x70_a279fb5c.jpg'
      }]
    }
  }
}
</script>

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
      width: 100%
</style>
