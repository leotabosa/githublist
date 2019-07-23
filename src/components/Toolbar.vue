<template>
  <div class="row">
    <Order @sortDataSet="sortTrigger($event)"> </Order>
    <Search @searchTermSet="searchTrigger($event)"></Search>
  </div>
</template>
<script>
import Search from './Search.vue'
import Order from './Order.vue'
export default {
  components: {
    Search,
    Order,
  },
  data() {
    return {
      searchTerm: null,
      sortData: {},
    }
  },
  methods: {
    searchTrigger(eventData) {
      this.$emit('searchTermSetting', eventData)
    },
    sortTrigger(eventData) {
      this.$emit('sortSetting', eventData)
    },
  },
}
</script>
<style scoped>
.row {
  padding-top: 10px;
  width: 100%;
}
</style>
