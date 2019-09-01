<template>
<div class='list' ref='wrapper'>
  <div>
    <div class='area'>
      <div class='title'>当前城市</div>
      <div class='button-list'>
        <div class='button-wrapper'>
          <div class='button'>北京</div>
        </div>
      </div>
    </div>
    <div class='area'>
      <div class='title '>热门城市</div>
      <div class='button-list'>
        <div class='button-wrapper' v-for='item of hot' :key='item.id'>
          <div class='button'>{{item.name}}</div>
        </div>
      </div>
    </div>
    <div class='area'>
      <div v-for='(item,key) of cities'
      :key='key'
      :ref="key"
      >
        <div class='title'>{{key}}</div>
        <div class="item" v-for='innerItem of item' :key=innerItem.id
        >
          {{innerItem.name}}
        </div>
      </div>
    </div>
  </div>
</div>
</template>
<script>
import Bscroll from 'better-scroll'
export default {
  name: 'CityList',
  props: {
    hot: Array,
    cities: Object,
    letter: String
  },
  mounted () {
    this.bet = new Bscroll(this.$refs.wrapper)
  },
  watch: {
    letter () {
      if (this.letter) {
        const element = this.$refs[this.letter][0]
        this.bet.scrollToElement(element)
      }
    }
  }
}
</script>
<style lang='stylus' scoped>
  .list
    position: absolute
    top: 4.75rem
    left: 0
    right: 0
    bottom: 0
    overflow: hidden
    .title
      line-height: 1.8rem
      background: #eee
      padding-left: 0.2rem
      color: #666
      font-size: 1rem
    .button-list
      overflow: hidden
      padding: 0.2rem 1.6rem 0.2rem 0.2rem
      .button-wrapper
        float: left
        width: 33.33%
        .button
          text-align: center
          margin: 0.4rem
          padding: 0.3rem 0;
          border-radius: 0.4rem;
          border: .04rem solid #000
    .item
      line-height: 1.7rem
      padding-left: 0.5rem
</style>
