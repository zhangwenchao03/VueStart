<template>
  <div class='swiper'>
    <swiper  :options="swiperOption" v-if='showSwiper'>
      <!-- slides -->
      <swiper-slide v-for="item of list" :key=item.id>
       <img class='swiper-image' :src='item.imgUrl'>
      </swiper-slide>
      <!-- Optional controls -->
      <div class="swiper-pagination"  slot="pagination"></div>
    </swiper>
  </div>

</template>

<script>
export default {
  name: 'HomeSwiper',
  props: {
    list: Array
  },
  data () {
    return {
      swiperOption: {
        pagination: '.swiper-pagination',
        loop: true
      }
    }
  },
  computed: {
    showSwiper () {
      return this.list.length
    }
  }
}
</script>

<style lang='stylus' scoped>
  .swiper >>> .swiper-pagination-bullet-active
    background: #fff
  .swiper
    overflow: hidden
    width: 100% !important
    height: 0
    padding-bottom: 53.4%
    .swiper-image
      width: 100%
</style>
