<template>
  <div class="textContainer">
    <strong>{{name}}</strong>
    <p>n°{{id}}</p>
  </div>
</template>

<script>

export default {
  name: 'CardText',
  props: {
    name: String,
    id: Number
  }
}
</script>

<style scoped>
.textContainer {
  margin-top: .3rem;
}
p {
  margin: 0;
  font-size: .8rem;
}
</style>
