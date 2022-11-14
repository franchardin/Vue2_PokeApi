<template>
  <div class="infoContainer">
    <!-- Conditional render if no pokemon is selected -->
    <div v-if="item?.id === undefined">
      <h1>No information yet.</h1>
      <p>Please search a pokemon to get its data.</p>
    </div>
    <div v-else>
      <h1>{{item.name}}<span class="subtitle"> n°{{item.id}}</span></h1>
      
      <div class="columnContainer">
        <div>
          <h2>Habilities</h2>
          <p v-for="(a, i) in item.abilities" :key="i">
            {{a.ability.name}}
          </p>
        </div>
        <div>
          <h2>Moves</h2>
          <p v-for="(m, i) in item.moves.slice(0, 4)" :key="i">
            {{m.move.name}}
          </p>
        </div>
        <div>
          <h2>Stats</h2>
          <p v-for="(s, i) in item.stats" :key="i" class="noTextWrap">
            <strong>{{s.stat.name}}:</strong> {{s.base_stat}}
          </p>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'DetailedInfo',
  data () {
    return {
      firstFourMoves: []
    }
  },
  props: {
    item: Object
  }
}
</script>

<style scoped>
.infoContainer{
  display: block;
  border-radius: 15px;
  padding: 1rem;
  min-width: 80vw;
  border: solid #3819c0 4px;
  box-shadow: inset #8777cc -4px -4px, #bbbbbb 3px 3px;
}
.columnContainer {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
}
.noTextWrap {
  white-space: nowrap;
}
h1 {
  margin: 0;
}
h1 span.subtitle {
  font-weight: 400;
  font-size: .8rem;
}
@media screen and (max-width: 720px) {
  .infoContainer {
    margin: 0 1rem;
    min-width: 80%;
  }
  .columnContainer {
    flex-direction: column;
  }
  h1 {
    font-size: 1.5rem;
  }
  h2 {
    font-size: 1.2rem;
  }
  p {
    font-size: .9rem;
  }
}
@media screen and (max-width: 350px) {
  .noTextWrap {
    white-space: pre-wrap;
  }
}
@media screen and (max-width: 250px) {
  .infoContainer {
    padding: 1rem;
    margin: 1rem;
    min-width: fit-content;
  }
  h1 {
    font-size: 14px;
  }
  h2 {
    font-size: 12px;
  }
  p {
    font-size: 12px;
  }
}
</style>
