<template>
  <div id="app">
    <TheHeader />
    <SearchBar @doSearch="doSearch" @doShowError="doShowError"/>
    <ErrorIndicator v-show="error" :message="errorMessage" />
    <loadingIndicator :loading="loading"/>
    <DetailsTable :items="initialArray" :initialSelectedItem="initialSelectedItem"/>
  </div>
</template>

<script>
import TheHeader from '@/components/TheHeader.vue'
import SearchBar from '@/components/SearchBar.vue'
import ErrorIndicator from '@/components/ErrorIndicator.vue'
import loadingIndicator from './components/loadingIndicator.vue'
import DetailsTable from './components/DetailsTable.vue'

export default {
  name: 'App',
  data () {
    return {
      initialArray: [],
      namesDataArray: [],
      newArray: [],
      showData: {},
      loading: true,
      error: false,
      errorMessage: '',
      url: 'https://pokeapi.co/api/v2/',
      initialSelectedItem: {}
    }
  },
  components: {
    TheHeader,
    SearchBar,
    ErrorIndicator,
    loadingIndicator,
    DetailsTable
  },
  mounted() {
      this.initialize()
  },
  methods: {
    async initialize() {
      this.getAllPokemonData()
      this.getInitialData()
    },
    // pokemons for the initial API request
    async getInitialData() {
      const initialPokemons = [
        {
          name: 'pikachu',
          url: 'https://pokeapi.co/api/v2/pokemon/25/'
        },
        {
          name: 'charmander',
          url: 'https://pokeapi.co/api/v2/pokemon/4/'
        },
        {
          name: 'ditto',
          url: 'https://pokeapi.co/api/v2/pokemon/132/'
        }
      ]
      initialPokemons.forEach(p => this.getInitialPokemonData(p.name, p.url))
      this.initialSelectedItem = this.initialArray.find(i => i.id === 25)
    },
    // gets initial pokemon's data from API or localStorage
    getInitialPokemonData(name, url) {
      const item = localStorage.getItem(name)
      if (item === null) {
        this.loading = true
        fetch(url)
          .then(res => (res.status, res.json()))
          .then(json => {
            this.initialArray.push(json)
            localStorage.setItem(name, JSON.stringify(json))
          })
          .catch(err => {
            console.error(err)
            this.error = true;
            this.errorMessage = err
          })
        setTimeout(() => {this.loading = false}, 600)
      } else {
        if(this.initialArray.find(i => i.id === JSON.parse(item).id) === undefined) {
          this.initialArray.push(JSON.parse(item))
        }
      }
    },
    // gets searched pokemons data in API or localStorage
    getAPokemonData(name, url) {
      const item = localStorage.getItem(name)
      if (item === null) {
        this.loading = true
        fetch(url)
          .then(res => (res.status, res.json()))
          .then(json => {
            this.initialArray = [json]
            localStorage.setItem(name, JSON.stringify(json))
          })
          .catch(err => {
            console.error(err)
            this.error = true;
            this.errorMessage = err
          })
        setTimeout(() => {this.loading = false}, 600)
      } else {
        if(this.initialArray.find(i => i.id === JSON.parse(item).id) === undefined) {
          this.initialArray = [JSON.parse(item)]
        }
      }
    },
    // gets name and url of all 1st generation pokemons
    async getAllPokemonData() {
      this.loading = true
      fetch(this.url + 'pokemon?limit=151')
        .then(res => (res.status, res.json()))
        .then(json => this.namesDataArray = json.results)
        .catch(err => {
          console.error(err)
          this.error = true;
          this.errorMessage = err
        })
      setTimeout(() => {this.loading = false}, 600)
    },
    // searches pokemon in 1st generation pokemons array
    doSearch(searchText) {
      if(searchText === '') {
        this.newArray = []
      } else {
        this.newArray = this.namesDataArray.filter(item => item.name.toLowerCase() === (searchText.toLowerCase()))
        if(this.newArray.length === 0) {
          this.doShowError(true, 'Pokemon does not exist. Please try again.')
        }
      }
      setTimeout(() => {this.loading = false}, 600)
    },
    // toggles error message
    doShowError (showError, message) {
      if (showError) {
        this.error = true
        this.errorMessage = message
      } else {
        this.error = false
        this.errorMessage = ''
      }
    }
  },
  watch: {
    // on pokemon search gets its data from API or localStorage
    newArray: {
      handler () {
        if(this.newArray.length > 0 ) {
          this.getAPokemonData(this.newArray[0].name, this.newArray[0].url, 'url')
        } else {
          this.initialArray = []
        }
      }
    }
  }
}
</script>

<style>
#app {
  padding: 2em 0;
  font-family: 'JetBrains Mono', 'Ubuntu Mono', monospace, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
/* Scrollbar styles (desktop) */
::-webkit-scrollbar {
  width: 10px;
}

/* Track */
::-webkit-scrollbar-track {
  box-shadow: inset 0 0 5px grey; 
  border-radius: 5px;
}
 
/* Handle */
::-webkit-scrollbar-thumb {
  background: #8777cc; 
  border-radius: 5px;
}

/* Handle on hover */
::-webkit-scrollbar-thumb:hover {
  background: #3819c0; 
}
/* End of Scrollbar styles (desktop) */
</style>
