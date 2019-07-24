<template>
  <div class="grid">
    <Card
      v-for="repo in repos"
      :key="repo.id"
      class="cards"
      :repo-name="repo.name"
      :repo-stars="repo.stargazers_count"
      :repo-u-r-l="repo.html_url"
      :repo-language="repo.language"
      :repo-description="repo.description"
    >
    </Card>
  </div>
</template>
<script>
import Card from './Card.vue'
export default {
  components: {
    Card,
  },
  props: {
    repos: {
      type: Array,
      required: true,
      default: () => [],
    },
  },
}
</script>
<style scoped>
.cards {
  margin-top: 20px;
  transition: 0.7s;
}
.grid {
  margin-bottom: 8vh;
  display: grid;
  grid-template-columns: repeat(auto-fit, 33%);
}
.cards:hover {
  box-shadow: 8px 6px 1px #3b4a54;
  transition: 0.7s;
}
</style>
