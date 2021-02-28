<template>
    <div class="container">
      <!-- Content Header (Page header) -->
      <section class="content-header">
        <h1>{{ Onglet }}</h1>
        <ol class="breadcrumb">
          <li><a>D&D</a></li>
          <li class="active">{{ Onglet }}</li>
        </ol>
      </section>

      <!-- Main content -->
      <section class="content">
        <hr>
        <div class="form-group" v-for="(value, title) in checkedElements" :key="title">
          <label class="form-check-label"><input class="form-check-input" type="checkbox" :value="value" v-on:input="checkUpdate($event.target.checked, title)" v-model="checkedElements[title]"> {{elTitles[title]}}</label>
        </div>
        <hr>
        <BooksSelection/>
      </section>
      <!-- /.content -->
    </div>
    <!-- /.container -->
</template>

<script>
import BooksSelection from './BooksSelection'
export default {
  name: 'Configuration',
  components: {BooksSelection},
  data () {
    return {
      Onglet: 'Configuration',
      elTitles: {
        schoolSearch: 'Rechercher par écoles',
        branchSearch: 'Rechercher par branches',
        classSearch: 'Rechercher par classes',
        levelSearch: 'Rechercher par niveaux'
      },
      checkedElements: {}
    }
  },
  created () {
    this.checkedElements = this.getCheckedElements()
  },
  methods: {
    getCheckedElements () {
      let tmp = JSON.parse(sessionStorage.getItem('checkedElements'))
      if (tmp == null) {
        tmp = {
          schoolSearch: false,
          branchSearch: false,
          classSearch: false,
          levelSearch: false
        }
      }
      return tmp
    },
    checkUpdate (val, title) {
      this.checkedElements[title] = val
      sessionStorage.setItem('checkedElements', JSON.stringify(this.checkedElements))
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
label {
  display: flex;
  justify-content: start;
  align-items: center;
}

input[type="checkbox"] {
  margin-right: .5em;
}
</style>
