<template>
  <div>
    <p>Error!</p>
    <p>{{message}}</p>
  </div>
</template>

<script>
export default {
  props: {
    message: [String, Error]
  }
}
</script>

<style scoped>
p {
  color: #bd0f0f;
}
</style>