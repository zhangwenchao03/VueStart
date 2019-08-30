<template>
  <div class='search'>
    <input type="text" class='search-input' placeholder="输入城市名称或拼音">
  </div>
</template>
<script>
export default {
  name: 'CitySearch'
}
</script>
<style lang='stylus' scoped>
  @import '~styles/variables.styl'
  .search
    height: 2.25rem
    background: $bgColor
    padding: 0 0.1rem
    .search-input
      box-sizing: border-box
      padding: 0 0.1rem
      border-radius: 0.2rem
      width: 100%
      height: 1.93rem
      line-height: 1.93rem
      text-align: center
      color: #666
</style>
