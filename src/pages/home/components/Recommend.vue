<template>
  <div>
    <div class='title'>
      热销推荐
    </div>
    <ul class='remove-gargin-padding'>
      <li v-for='item of list' :key='item.id'>
        <div class='item border-bottom'>
          <img class='item-image' :src='item.imgUrl'>
        <div class='item-info'>
          <p class='item-title'>{{item.title}}</p>
          <p class='item-desc'>{{item.desc}}</p>
          <button class='item-btn'>查看详情</button>
      </div>
    </div>
      </li>
    </ul>

  </div>
</template>
<script>
export default {
  name: 'HomeRecommend',
  props: {
    list: Array
  }
}
</script>
<style lang='stylus' scoped>
  .title
    margin-top: 0.1rem
    background: #eee
    line-height: 1.4rem
    text-indent: 0.2rem
    color: #333
  .remove-gargin-padding
    margin: 0 0
    padding: 0 0
  .item
    display: flex
    overflow: hidden
    height: 7rem
    .item-image
      height: 6.5rem
      padding: 0.2rem
    .item-info
      flex: 1
      padding: 0.2rem
      .item-title
        margin: 0.4rem 0
        line-height: 1.2rem
      .item-desc
        margin: 0.4rem 0
        line-height: 1.2rem
        color: #ccc
      .item-btn
        border-radius: 0.01rem
        color: #fff
        padding: 0.1rem
        background: #ff9300
</style>
