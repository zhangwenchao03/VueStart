<template>
  <div class='icons'>
    <swiper>
      <!-- slides -->
      <swiper-slide v-for="(page,index) of pages" :key='index'>
        <div class='icon' v-for='item of page' :key='item.id'>
          <div class='icon-image'>
            <img class='image-content' :src='item.imgUrl'>
          </div>
         <p class='icon-desc'>{{item.imgDesc}}</p>
        </div>
      </swiper-slide>
    </swiper>
    <div class='icon' v-for='item of IconList' :key='item.id'>
      <div class='icon-image'>
        <img class='image-content' :src='item.imgUrl'>
      </div>
      <p class='icon-desc'>{{item.imgDesc}}</p>
    </div>
  </div>
</template>
<script>
export default {
  name: 'HomeIcons',
  data () {
    return {
      IconList: [{
        id: '001',
        imgUrl: 'https://s.qunarzz.com/homenode/images/touchheader/hotel.png',
        imgDesc: '酒店'
      }, {
        id: '002',
        imgUrl: 'https://s.qunarzz.com/homenode/images/touchheader/hotel.png',
        imgDesc: '酒店'
      }, {
        id: '003',
        imgUrl: 'https://s.qunarzz.com/homenode/images/touchheader/hotel.png',
        imgDesc: '酒店'
      }, {
        id: '004',
        imgUrl: 'https://s.qunarzz.com/homenode/images/touchheader/hotel.png',
        imgDesc: '酒店'
      }, {
        id: '005',
        imgUrl: 'https://s.qunarzz.com/homenode/images/touchheader/hotel.png',
        imgDesc: '酒店'
      }, {
        id: '006',
        imgUrl: 'https://s.qunarzz.com/homenode/images/touchheader/hotel.png',
        imgDesc: '酒店'
      }, {
        id: '007',
        imgUrl: 'https://s.qunarzz.com/homenode/images/touchheader/hotel.png',
        imgDesc: '酒店'
      }, {
        id: '008',
        imgUrl: 'https://s.qunarzz.com/homenode/images/touchheader/hotel.png',
        imgDesc: '酒店'
      }, {
        id: '009',
        imgUrl: 'https://s.qunarzz.com/homenode/images/touchheader/hotel.png',
        imgDesc: '酒店'
      }]
    }
  },
  computed: {
    pages () {
      const pgs = []
      this.IconList.forEach(
        (item, index) => {
          let i = Math.floor(index / 8)
          if (!pgs[i]) {
            pgs[i] = []
          }
          pgs[i].push(item)
        })
      return pgs
    }
  }
}
</script>
<style lang="stylus" scoped>
  .icons
    overflow: hidden
    width: 100%
    height: 0
    padding-bottom: 50%
    .icon
      position: relative
      float: left
      overflow: hidden
      width: 25%
      height: 0
      padding-bottom: 25%
      .icon-image
        position: absolute
        top: 0
        left: 0
        right: 0
        bottom: 1.2rem
        box-sizing: border-box
        padding: 0.1rem
        .image-content
          display: block
          margin: 0 auto
          height: 100%
      .icon-desc
        position: absolute
        left: 0
        right: 0
        bottom: 0
        height: 1.2rem
        margin: 0
        text-align: center
</style>
