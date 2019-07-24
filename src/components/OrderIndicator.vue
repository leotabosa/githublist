<template
  ><span class="popup"
    ><p class="popup-text">{{ indicator }}</p
    ><p></p
  ></span>
</template>
<script>
export default {
  props: {
    indicator: {
      type: String,
      required: true,
      default: () => '',
    },
  },
}
</script>
<style scoped>
.popup {
  text-align: center;
  position: fixed;
  width: 120px;
  height: 40px;
  left: calc(25% - 60px);
  border: 2px solid white;
  border-radius: 20px;
  background-color: black;
  z-index: 1;
  animation: show 1.8s;
  opacity: 0;
}
@keyframes show {
  0% {
    opacity: 0;
    width: 0px;
    border-radius: 30px;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
  }
  50% {
    opacity: 0.6;
    width: 120px;
    border-radius: 30px;
  }
  100% {
    opacity: 0;
  }
}
.popup-text {
  padding-top: 5px;
  color: white;
}
@media screen and (max-width: 768px) {
  .popup {
    visibility: hidden;
  }
}
@media screen and (max-width: 1024px) {
  .popup {
    text-align: center;
    position: fixed;
    width: 120px;
    height: 40px;
    left: calc(20% - 60px);
    border: 2px solid white;
    border-radius: 20px;
    background-color: black;
    z-index: 1;
    animation: show 1.5s ease-in-out;
    opacity: 0;
  }
}
</style>
