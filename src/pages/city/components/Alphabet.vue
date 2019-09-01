
<template>
<div>
  <ul class='alpha-list'>
    <li class='item'
    v-for='(item,key) of cities'
    :key='key'
    :ref='key'
    @click='handleLiClick'
    @touchstart="handleTouchStart"
    @touchmove="handleTouchMove"
    @touchend="handleTouchEnd"
    >{{key}}
   </li>
  </ul>
</div>
</template>
<script>
export default {
  name: 'Alphabet',
  props: {
    cities: Object,
    letters: Array
  },
  computed: {
    letters () {
      const letters = []
      for (let i in this.cities) {
        letters.push(i)
      }
      return letters
    }
  },
  updated () {
    this.startY = this.$refs['A'][0].offsetTop
  },
  methods: {
    handleLiClick (e) {
      this.$emit('change', e.target.innerText)
    },
    handleTouchStart () {
      this.touchMoveStart = true
    },
    handleTouchMove (e) {
      if (this.touchMoveStart) {
        if (this.timer) {
          clearTimeout(this.timer)
        }
        this.timer = setTimeout(() => {
          const touchY = e.touches[0].clientY - 76
          const index = Math.floor((touchY-this.startY)/23)
          this.$emit('change', this.letters[index])
        },20)
      }
    },
    handleTouchEnd () {
      this.touchMoveStart = false
    }
  },
  data () {
    return{
    touchMoveStart: false,
    timer: null,
    startY: 0
    }

  }
}
</script>
<style lang='stylus' scoped>
  @import '~styles/variables.styl'
  .alpha-list
    display: flex
    flex-direction: column
    justify-content: center
    position: absolute
    margin: 0
    top: 4.75rem
    right: 0
    bottom: 0
    width: 2rem
    .item
      display: block
      line-height: 1.45rem
      text-align: center
      color: $bgColor
</style>
