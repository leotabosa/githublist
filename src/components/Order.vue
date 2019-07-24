<template>
  <div class="btn-group" role="group">
    <button
      id="order-button-1"
      type="button"
      class="btn btn-dark btn-order"
      @click="sort('stargazers_count')"
      >Estrelas
      <span
        v-if="
          sortPref.property === 'stargazers_count' &&
            sortPref.type === 'Crescente'
        "
        class="star-indicator"
        >&#x2191;</span
      >
      <span
        v-if="
          sortPref.property === 'stargazers_count' &&
            sortPref.type === 'Decrescente'
        "
        class="star-indicator"
        >&#x2193;</span
      >
    </button>
    <button
      id="order-button-2"
      type="button"
      class="btn btn-dark btn-order"
      style="border-radius:2px"
      @click="sort('language')"
      >Linguagem
      <span
        v-if="sortPref.property === 'language' && sortPref.type === 'Crescente'"
        class="language-indicator"
      >
        &#x2191;
      </span>
      <span
        v-if="
          sortPref.property === 'language' && sortPref.type === 'Decrescente'
        "
        class="language-indicator"
      >
        &#x2193;
      </span>
    </button>
    <OrderIndicator
      v-if="indicator"
      :indicator="sortPref.type"
    ></OrderIndicator>
  </div>
</template>

<script>
import OrderIndicator from './OrderIndicator.vue'
export default {
  components: {
    OrderIndicator,
  },
  data() {
    return {
      sortPref: {
        property: 'stargazers_count',
        type: 'Decrescente',
      },
      indicator: false,
    }
  },
  methods: {
    // verificações da função de ordenação
    sort(prop) {
      document.getElementById('order-button-1').disabled = true
      document.getElementById('order-button-2').disabled = true
      this.indicator = true
      if (this.sortPref.property === prop) {
        this.sortPref.type =
          this.sortPref.type === 'Crescente' ? 'Decrescente' : 'Crescente'
      } else {
        this.sortPref.property = prop
        this.sortPref.type = 'Crescente'
      }
      this.$emit('sortDataSet', this.sortPref)
      setTimeout(this.indicatorFalse, 1200)
    },
    indicatorFalse() {
      document.getElementById('order-button-1').disabled = false
      document.getElementById('order-button-2').disabled = false
      this.indicator = false
    },
  },
}
</script>

<style scoped>
.btn-group {
  padding-left: 10px;
  margin-left: auto;
}
.btn-group button {
  border-radius: 20px;
}
.btn-dark {
  background: black;
  transition: 0.4s;
}
.btn-dark:hover {
  background: #3b4a54;
  transition: 0.4s;
}
.star-indicator {
  display: inline;
}
.language-indicator {
  display: inline;
}
@media screen and (max-width: 768px) {
  .btn-group {
    margin-left: 0;
  }
  .btn-group button {
    width: 30.5vw;
  }
}
</style>
