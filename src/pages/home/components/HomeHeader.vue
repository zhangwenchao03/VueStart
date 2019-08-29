<template>
  <div class='header'>
    <div class='header-left'>
     <div class="iconfont iconfanhui back-arrow"></div>
    </div>
    <div class='header-input'>
      <span class="iconfont iconsousuo"></span>
    shuru</div>
    <router-link to='/city'>
      <div class='header-right'>
      city
      <span class="iconfont iconarrow-down down-arrow"></span>
      </div>
    </router-link>

  </div>
</template>

<script>
export default {
  name: 'HomeHeader'
}
</script>
<!-- scoped表示只在当前组件范围起作用 -->
<style lang="stylus" scoped>
  @import '~styles/variables.styl'
  .header
    display: flex
    height: 2.68rem
    line-height: 2.68rem
    background: $bgColor
    color: #fff
    .header-left
      width: 2rem
      float: left
      .back-arrow
        text-align: center
        font-size: 1.2rem
    .header-input
      flex: 1
      line-height: 2.28rem
      height: 2.28rem
      background: #fff
      margin-top: 0.2rem
      margin-left: 0.2rem
      padding-left: 0.2rem
      border-radius: 0.3rem
      color: #ccc
    .header-right
      width: 3.875rem
      float: right
      text-align: center
      .down-arrow
        margin-left: -0.1rem
</style>
