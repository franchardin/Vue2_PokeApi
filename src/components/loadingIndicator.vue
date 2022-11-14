<template>
  <div class="loadingIndicator">
    <img v-show="loading" class="loaderImage" :src="require('@/assets/loader-icon-b-48.png')"/>
  </div>
</template>

<script>
export default {
  name: 'loadingIndicator',
  props: {
    loading: {
      type: Boolean,
      default: false
    }
  }
}
</script>

<style scoped>
.loadingIndicator {
  z-index: 10;
  height: 48px;
}
.loaderImage {
  animation: rotate 1.5s linear infinite;
}
@keyframes rotate {
  100% {
    transform: rotate(360deg); 
  }
}
</style>
