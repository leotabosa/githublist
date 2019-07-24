<template>
  <form class="form-inline my-2 my-lg-0">
    <input
      v-model="searchTerm"
      class="form-control mr-sm-2"
      type="search"
      placeholder="Buscar"
      @keydown.enter.prevent.stop
      @keydown="setTime(sendSearchTerm)"
    />
  </form>
</template>
<script>
export default {
  data() {
    return {
      searchTerm: null,
    }
  },
  methods: {
    sendSearchTerm() {
      this.$emit('searchTermSet', this.searchTerm)
    },
    setTime(func) {
      clearTimeout(this.interval)
      this.interval = setTimeout(func, 500)
    },
  },
}
</script>
<style scoped>
.form-control:focus {
  border-radius: 50px;
  transition: 0.8s;
  border: 1px solid green;
}
.form-control:not(:focus) {
  border-radius: 0px;
  transition: 0.4s;
}
.form-inline {
  padding-left: 10px;
  margin-right: auto;
}
@media screen and (max-width: 768px) {
  .form-inline {
    width: 26.8vw;
  }
}
</style>
