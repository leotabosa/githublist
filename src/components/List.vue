<template>
  <div class="row">
    <div v-for="repo in repos" :key="repo.id" class="cards-list col-sm-4">
      <Card
        class="cards"
        :repoName="repo.name"
        :repoStars="repo.stargazers_count"
        :repoURL="repo.html_url"
        :repoLanguage="repo.language ? repo.language : ''"
        :repoDescription="repo.description ? repo.description : ''"
      >
      </Card>
    </div>
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
}
.row {
  margin-bottom: 8vh;
}
</style>
