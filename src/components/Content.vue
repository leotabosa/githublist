<template>
  <div>
    <Toolbar
      @searchTermSetting="sendMiddleSearchTerm($event)"
      @sortSetting="sendMiddleSortData($event)"
    >
    </Toolbar>
    <List :repos="repos"></List>
  </div>
</template>

<script>
import Toolbar from './Toolbar.vue'
import List from './List.vue'
export default {
  components: {
    Toolbar,
    List,
  },
  props: {
    repos: {
      type: Array,
      required: true,
      default: () => [],
    },
  },
  methods: {
    sendMiddleSearchTerm(eventData) {
      this.$emit('onSearch', eventData)
    },
    sendMiddleSortData(eventData) {
      this.$emit('onSort', eventData)
    },
  },
}
</script>
