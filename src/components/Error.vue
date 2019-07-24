<template>
  <div class="error-wrap">
    <h2 class="error-message">{{ errorMessage }}</h2>
    <a href="https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Status/403"
      ><p class="error-link">Clique para mais informações do erro</p>
    </a>
  </div>
</template>

<script>
export default {
  props: {
    errorMessage: {
      type: Error,
      default: () => '',
      required: true,
    },
  },
}
</script>

<style scoped>
.error-wrap {
  position: absolute;
  height: 100vh;
  width: 100%;
  z-index: 1;
  background-color: white;
}
.error-message {
  margin-top: 30px;
  margin-left: 30px;
  color: red;
}
.error-link {
  margin-left: 30px;
  color: black;
  font-size: 18px;
}
</style>
