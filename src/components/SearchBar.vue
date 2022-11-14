<template>
  <div class="searchBar">
    <input class="input" v-model="searchText" @keyup.enter="doSearch" />
    <button class="button" @click="doSearch"><img src="@/assets/magnifier-r.png" /></button>
  </div>
</template>

<script>
export default {
  name: 'SearchBar',
  data () {
    return {
      searchText: ''
    }
  },
  methods: {
    // doSearch method and error handling
    doSearch () {
      if(this.searchText !== '') {
        this.$emit('doShowError', false, '')
        this.$emit('doSearch', this.searchText)
        this.searchText = ''
      } else {
        this.$emit('doSearch', this.searchText)
        this.$emit('doShowError', true, "You must write a pokemon's name before searching")
      }
    }
  }
}
</script>

<style scoped>
.searchBar {
  margin-bottom: 1rem;
}
.input {
  height: 35px;
  border-radius: 15px;
  border: solid #3819c0 4px;
  box-shadow: inset #8777cc -2px -2px, #bbbbbb 3px 3px;
  padding: 0 8px;
  font-family: 'JetBrains Mono', 'Ubuntu Mono', monospace, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
.input:focus-visible {
  outline: none;
}
.button {
  border: solid #bd0f0f 4px;
  border-radius: 15px;
  height: 45px;
  width: 45px;
  background: none;
  vertical-align: middle;
  padding-top: 5px;
  margin-left: 5px;
  box-shadow: inset #cd5c5c -2px -2px,#bbbbbb 3px 3px;
}
.button:hover {
  background: #f7eaea;
}
.button:active {
  transform: translate(3px, 3px);
  box-shadow: inset #cd5c5c -2px -2px;
}
img {
  height: 24px;
  width: 24px;
}
@media screen and (max-width: 281px) {
  .input {
    max-width: 80%;
  }
  .button {
    width: 50%;
    margin-top: 8px;
  }
}
</style>
