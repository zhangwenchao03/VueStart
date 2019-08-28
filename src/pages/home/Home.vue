<template>
<div >
     <home-header></home-header>
<<<<<<< HEAD
     <home-swiper></home-swiper>
=======
     <home-swiper :list='swiperList'></home-swiper>
     <home-icons :list='iconList'></home-icons>
     <home-recommend :list='recommendList'></home-recommend>
     <home-weekend :list='weekendList'></home-weekend>
>>>>>>> origin/VueBranch
</div>
</template>

<script>
import HomeHeader from './components/HomeHeader'
import HomeSwiper from './components/HomeSwiper'
<<<<<<< HEAD
=======
import HomeIcons from './components/HomeIcons'
import HomeRecommend from './components/Recommend'
import HomeWeekend from './components/Weenkend'
import axios from 'axios'
>>>>>>> origin/VueBranch
export default {
  name: 'Home',
  components: {
    HomeHeader,
<<<<<<< HEAD
    HomeSwiper
=======
    HomeSwiper,
    HomeIcons,
    HomeRecommend,
    HomeWeekend
  },
  data () {
    return {
      swiperList: [],
      iconList: [],
      recommendList: [],
      weekendList: []
    }
  },
  methods: {
    getHomeInfo () {
      axios.get('/api/index.json')
        .then(this.getHomeInfoSucc)
    },
    getHomeInfoSucc (res) {
      res = res.data
      if (res.ret && res.data) {
        const data = res.data
        this.swiperList = data.swiperList
        this.iconList = data.iconList
        this.recommendList = data.recommendList
        this.weekendList = data.weekendList
      }
    }
  },
  mounted () {
    this.getHomeInfo()
>>>>>>> origin/VueBranch
  }
}
</script>
