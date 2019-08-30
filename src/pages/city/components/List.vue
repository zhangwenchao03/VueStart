<template>
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
    <div v-for='(item,key) of cities' :key='key'>
      <div class='title'>{{key}}</div>
      <div class="item" v-for='innerItem of item' :key=innerItem.id>
        {{innerItem.name}}
      </div>
    </div>

  </div>
</div>
</template>
<script>
export default {
  name: 'CityList',
  props: {
    hot: Array,
    cities: Object
  }
}
</script>
<style lang='stylus' scoped>
  .title
    line-height: 1.8rem
    background: #eee
    padding-left: 0.2rem
    color: #666
    font-size: 1rem
  .button-list
    overflow: hidden
    padding: 0.2rem
    .button-wrapper
      float: left
      width: 33.33%
      .button
        text-align: center
        margin: 0.4rem
        padding: 0.3rem 0;
        border-radius: 0.4rem;
        border: .02rem solid #000
  .item
    line-height: 1.7rem
    padding-left: 0.5rem
</style>
