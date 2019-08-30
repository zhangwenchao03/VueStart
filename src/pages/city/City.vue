<template>
<div>
  <city-header></city-header>
  <city-search></city-search>
  <city-list
    :hot='hotCities'
    :cities='cities'
  ></city-list>
</div>
</template>
<script>
import axios from 'axios'
import CityHeader from './components/Header'
import CitySearch from './components/Search'
import CityList from './components/List'
export default {
  name: 'City',
  components: {
    CityHeader,
    CitySearch,
    CityList
  },
  data () {
    return {
      city: {},
      cities: {},
      hotCities: []
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
    }
  },
  mounted: function () {
    this.getCityInfo()
  }
}
</script>
<style lang='stylus' scoped>
</style>
