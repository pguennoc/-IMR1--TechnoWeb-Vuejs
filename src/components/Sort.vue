<template>
  <div class="spell">
    <h5 @click="show = !show" class="p-2">{{ spell[1] }}</h5>
    <ul class="spellDetail" v-if="show">
      <li v-for="(prop, index) in spell" v-bind:key="index">
        <strong>{{ categories[index] }}</strong> : {{ prop }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'Sort',
  props: ['spell', 'index'],
  data () {
    return {
      categories: [
        'Livre',
        'Nom',
        'Ecole',
        'Branches',
        'Classes',
        'Composantes',
        'Temps d:\'incantation',
        'Portée',
        'Cible',
        'Durée',
        'Jet de sauvegarde',
        'Résistance à la magie',
        'Description',
        'Nécessaire'
      ],
      show: false
    }
  }
}
</script>
