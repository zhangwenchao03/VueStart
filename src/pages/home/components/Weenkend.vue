<template>
  <div>
    <div class='title'>
      周末去哪儿
    </div>
    <ul class="remove-default">
      <li v-for='item of list' :key='item.id'>
        <div class='item-image-wraper'>
          <img class='item-image' :src="item.imgUrl">
        </div>
        <div class='item-info'>
          <p class="item-title">{{item.title}}</p>
          <p class="item-desc">{{item.desc}}</p>
        </div>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  name: 'HomeWeekend',
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
  .remove-default
    padding: 0 0
    margin: 0 0
    .item-image-wraper
      overflow: hidden
      width: 100%
      height: 0
      padding-bottom: 53.4%
      .item-image
        width: 100%
    .item-info
      padding: .1rem
      .item-title
        line-height: .54rem
        font-size: .32rem
      .item-desc
        line-height: .4rem
        color: #ccc
</style>
