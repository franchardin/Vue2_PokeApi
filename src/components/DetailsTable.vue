<template>
  <header class="DetailsTable" :class="{'row': items.length > 1}">
    <div class="mainCard" v-for="item in items" :key="item.id">
      <CardImage :imageSrc="item.sprites.front_default" @clickImage="clickImage(item.id)"/>
      <CardText :name="item.name" :id="item.id"/>
    </div>
    <DetailedInfo :item="selectedItem"/>
  </header>
</template>

<script>
import CardImage from '@/components/CardImage.vue'
import CardText from '@/components/CardText.vue'
import DetailedInfo from '@/components/DetailedInfo.vue'

export default {
  name: 'DetailsTable',
  components: {
    CardImage,
    CardText,
    DetailedInfo
  },
  data () {
    return {
      searchText: '',
      selectedItem: this.items.length > 0 ? this.items[0] : null,
      isInitial: true
    }
  },
  props: {
    items: Array
  },
  methods: {
    clickImage(id) {
      this.showThisPokemonData(id)
    },
// shows selected pokemon's data in table
    showThisPokemonData (id) {
      this.selectedItem = this.items.filter(item => item.id === id)[0]
    },
    // shows initial selected pokemon's data in table (pikachu's data)
    showInitialPokemonData () {
      if (this.items.filter(item => item.id === 25)[0] !== undefined) {
        this.selectedItem = this.items.filter(item => item.id === 25)[0]
        this.isInitial = false
      }
    }
  },
  watch: {
    searchText: {
      handler () {
        this.$emit('doSearch', this.searchText)
      }
    },
    items: {
      handler () {
        if(this.items[0] !== undefined) {
          this.isInitial
            ? this.showInitialPokemonData()
            : this.showThisPokemonData (this.items[0].id)
        } else {
          this.selectedItem = null
        }
      }
    }
  }
}
</script>

<style scoped>
.DetailsTable {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  flex-wrap: wrap;
  padding: 0 2rem;
}
.DetailsTable.row {
  flex-direction: row;
}
.mainCard {
  margin: 1rem;
}
@media screen and (max-width: 250px) {
  .DetailsTable {
    padding: 0;
  }
}
</style>
