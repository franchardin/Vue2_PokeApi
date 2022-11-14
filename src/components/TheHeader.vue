<template>
  <div class="headerContainer">
    <img src="https://raw.githubusercontent.com/PokeAPI/media/master/logo/pokeapi_256.png" alt="image with pokeapi logo in blue and yellow"/>
  </div>
</template>

<script>

export default {
  name: 'TheHeader',
  props: {
    imageSrc: String
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
}
@media screen and (max-width: 200px) {
  .headerContainer {
    padding-right: 6px;
  }
}
</style>
