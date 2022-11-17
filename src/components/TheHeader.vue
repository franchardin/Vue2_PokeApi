<template>
  <div class="headerContainer" title="Restart app">
    <img @click="restartApp" src="https://raw.githubusercontent.com/PokeAPI/media/master/logo/pokeapi_256.png" alt="image with pokeapi logo in blue and yellow"/>
  </div>
</template>

<script>

export default {
  name: 'TheHeader',
  props: {
    imageSrc: String
  },
  methods: {
    restartApp() {
      this.$emit('restartApp')
    }
  }
}
</script>

<style scoped>
.headerContainer {
  margin: 1em 0;
  padding-right: 12px;
}
img {
  max-width: 80vw;
  height: auto;
  cursor: pointer;
}
@media screen and (max-width: 200px) {
  .headerContainer {
    padding-right: 6px;
  }
}
</style>
