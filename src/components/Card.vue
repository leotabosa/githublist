<template>
  <div class="card">
    <div class="card-body">
      <h5 class="card-title" :title="repoName">{{ repoName }}</h5>
      <p class="card-text">
        <br /><b>Número de estrelas:</b> {{ repoStars }} <br />
        <b>Linguagem:</b> {{ repoLanguage }}
      </p>
      <p class="description"><b>Descrição:</b> {{ repoDescription }}</p>
      <a :href="repoURL" class="btn btn-dark" target="_blank"
        >Ir para o repositório</a
      >
    </div>
  </div>
</template>
<script>
export default {
  props: {
    repoName: {
      type: String,
      required: true,
    },
    repoStars: {
      type: Number,
      required: true,
    },
    repoLanguage: {
      type: String,
      default: () => '',
    },
    repoURL: {
      type: String,
      required: true,
    },
    repoDescription: {
      type: String,
      default: () => '',
    },
  },
}
</script>
<style scoped>
.card {
  border-top: 1px solid black;
  border-bottom: 1px solid black;
  margin-left: 10px;
  margin-right: 10px;
}
.btn-dark {
  background: black;
  border-radius: 50px;
  transition: 0.4s;
}
.btn-dark:hover {
  background: #3b4a54;
  transition: 0.4s;
}
.description {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
.card-title {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
</style>
