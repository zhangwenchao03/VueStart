<template>
<div>
  <city-header></city-header>
  <city-search></city-search>
  <city-list
    :hot='hotCities'
    :cities='cities'
    :letter='letter'
  ></city-list>
  <alphabet :cities='cities'
  @change='handleLetterChange'></alphabet>
</div>
</template>
<script>
import axios from 'axios'
import CityHeader from './components/Header'
import CitySearch from './components/Search'
import CityList from './components/List'
import Alphabet from './components/Alphabet'
export default {
  name: 'City',
  components: {
    CityHeader,
    CitySearch,
    CityList,
    Alphabet
  },
  data () {
    return {
      city: {},
      cities: {},
      hotCities: [],
      letter: ''
    }
  },
  methods: {
    getCityInfo () {
      axios.get('/api/city.json')
        .then(this.handleGetCityInfo)
    },
    handleGetCityInfo (res) {
      res = res.data
      if (res.ret && res.data) {
        const data = res.data
        this.cities = data.cities
        this.hotCities = data.hotCities
      }
    },
    handleLetterChange (l) {
      this.letter = l
    }
  },
  mounted: function () {
    this.getCityInfo()
  }
}
</script>
<style lang='stylus' scoped>
</style>
