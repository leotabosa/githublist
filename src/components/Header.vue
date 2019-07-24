<template>
  <div>
    <nav class="navbar navbar-dark bg-custom">
      <a id="navbar-brand-1" class="navbar-brand" href=""
        >Voltar à página inicial</a
      >
      <a
        id="navbar-title"
        class="navbar-brand"
        href=""
        style="color:white; font-size:22px;"
        >Repositórios da Microsoft</a
      >
      <a
        id="navbar-brand-2"
        class="navbar-brand"
        href="https://github.com/Microsoft"
        >GitHub da Microsoft</a
      >
    </nav>
  </div>
</template>

<style scoped>
nav {
  border-bottom-left-radius: 20px;
  border-bottom-right-radius: 20px;
  border-bottom: 3px solid green;
}
.bg-custom {
  background-color: black;
}
.navbar {
  position: relative;
}
.navbar-brand:hover {
  font-size: 20.5px;
  transition: 0.3s;
}
.navbar-brand:not(hover) {
  font-size: 20px;
  transition: 0.3s;
}

@media screen and (max-width: 767px) {
  #navbar-brand-1 {
    visibility: hidden;
  }
  #navbar-brand-2 {
    visibility: hidden;
  }
  #navbar-title {
    position: absolute;
    z-index: 1;
    top: 10px;
    text-align: center;
    width: 94%;
  }
  .navbar {
    height: 60px;
  }
}
</style>
