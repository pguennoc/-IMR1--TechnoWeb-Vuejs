<template>
  <div class="searched-item">
    <p>Sorts trouvés : {{ results.length }}</p>
    <hr>
    <ul>
      <li v-bind:key="index" v-for="(result, index) in results">
        <Sort v-bind:spell="result" v-bind:index="index"/>
      </li>
    </ul>
    <p v-if="!results.length">Aucun résultat</p>
  </div>
</template>

<script>
import Sort from './Sort'
export default {
  name: 'Resultat',
  props: ['results'],
  components: {Sort}
}
</script>

<style scoped>
ul {
  list-style-type: none;
  padding: 0;
  margin: 0;
}

li {
  cursor: pointer;
}
</style>
