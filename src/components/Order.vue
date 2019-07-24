<template>
  <div class="btn-group" role="group">
    <button
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
  </div>
</template>

<script>
export default {
  data() {
    return {
      sortPref: {
        property: 'stargazers_count',
        type: 'Decrescente',
      },
    }
  },
  methods: {
    // verificações da função de ordenação
    sort(prop) {
      if (this.sortPref.property === prop) {
        this.sortPref.type =
          this.sortPref.type === 'Crescente' ? 'Decrescente' : 'Crescente'
      } else {
        this.sortPref.property = prop
        this.sortPref.type = 'Crescente'
      }
      this.$emit('sortDataSet', this.sortPref)
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
</style>
