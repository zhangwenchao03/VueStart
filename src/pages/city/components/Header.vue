<template>
<div class='header'>
  城市选择
  <router-link to='./'>
    <div class="header-back iconfont iconfanhui back-arrow"></div>
  </router-link>
</div>
</template>
<script>
export default {
  name: 'CityHeader'
}
</script>
<style lang='stylus' scoped>
  @import '~styles/variables.styl'
  .header
    height: 2.5rem
    line-height: 2.5rem
    background: $bgColor
    text-align: center
    color: #fff
    .header-back
      position: absolute
      top: 0
      left: 0.25rem
      font-size: 1.2rem
      color: #fff
</style>
