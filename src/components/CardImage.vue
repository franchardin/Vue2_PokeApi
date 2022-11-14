<template>
  <div @click="clickImage" class="imageContainer">
    <img :src="imageSrc" :alt="imageSrc + ' image'"/>
  </div>
</template>

<script>

export default {
  name: 'PokemonImage',
  props: {
    imageSrc: String
  },
  methods: {
    clickImage() {
      this.$emit('clickImage')
    }
  }
}
</script>

<style scoped>
.imageContainer{
  border-radius: 50%;
  width: 6rem;
  height: 6rem;
  border: solid rgb(189, 15, 15) 4px;
  box-shadow: inset #cd5c5c -4px -4px,
              #bbbbbb 3px 3px;
}
.imageContainer:hover {
  transform: scale(1.05);
}
img:hover {
  filter: brightness(1.2);
}
</style>
