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
        <div class="searchName form-group">
          <label>Nom</label>
          <input class="form-control" v-model="nameSearch" v-on:input="search()" placeholder="Recherche">
        </div>
        <div class="row">
          <RechercheElements v-if="checkedElements.schoolSearch" v-model="selectedSchool" v-bind:array="schools" v-bind:label="'Écoles'"/>
          <RechercheElements v-if="checkedElements.branchSearch" v-model="selectedBranch" v-bind:array="branches" v-bind:label="'Branches'"/>
          <RechercheElements v-if="checkedElements.classSearch" v-model="selectedClass" v-bind:array="classes" v-bind:label="'Classes'"/>
          <RechercheElements v-if="checkedElements.levelSearch" v-model="selectedLevel" v-bind:array="levels" v-bind:label="'Niveaux'"/>
        </div>
        <hr>
        <Resultat v-bind:results="results"/>
      </section>
      <!-- /.content -->
    </div>
    <!-- /.container -->
</template>

<script>
import RechercheElements from './RechercheElements'
import Resultat from './Resultat'
export default {
  name: 'Recherche',
  components: {RechercheElements, Resultat},
  data () {
    return {
      Onglet: 'Recherche',
      nameSearch: '',
      checkedElements: {},
      selectedBooks: [],
      schools: [],
      branches: [],
      classes: [],
      levels: [],
      selectedSchool: '',
      selectedBranch: '',
      selectedClass: '',
      selectedLevel: '',
      results: []
    }
  },
  created () {
    this.checkedElements = JSON.parse(sessionStorage.getItem('checkedElements')) || {}
    this.selectedBooks = JSON.parse(sessionStorage.getItem('selectedBooks')) || {}
    this.schools = this.getTable(2)
    this.branches = this.getTable(3).flat().filter(onlyUnique).sort()
    this.classes = this.getTableAdvanced(0)
    this.levels = this.getTableAdvanced(1)
  },
  mounted () {
    this.search()
  },
  methods: {
    getTable (index) {
      let tmp = []
      sortTable.forEach((el) => {
        tmp.push(el[index])
      })
      return tmp.filter(onlyUnique).sort()
    },
    getTableAdvanced (index) {
      let tmp = []
      this.getTable(4).forEach((a) => {
        a.forEach((el) => {
          tmp.push(el[index])
        })
      })
      return tmp.filter(onlyUnique).sort()
    },
    getResult () {
      let tab = sortTable
      tab = tab.filter(booksFilter, this.selectedBooks)

      if (this.checkedElements.schoolSearch === true) tab = tab.filter(schoolFilter, this.selectedSchool)
      if (this.checkedElements.branchSearch === true) tab = tab.filter(branchFilter, this.selectedBranch)
      if (this.checkedElements.classSearch === true) tab = tab.filter(classFilter, this.selectedClass)
      if (this.checkedElements.levelSearch === true) tab = tab.filter(levelFilter, this.selectedLevel)
      tab = tab.filter(nameFilter, this.nameSearch.toLowerCase())

      return tab
    },
    search () {
      this.results = this.getResult()
    }
  }
}

function onlyUnique (value, index, self) {
  return self.indexOf(value) === index
}

function booksFilter (currElt) {
  return this.indexOf(currElt[0]) !== -1
}

function nameFilter (currElt) {
  return currElt[1].toLowerCase().indexOf(this) > -1
}

function schoolFilter (currElt) {
  return currElt[2].toLowerCase() === this.toLowerCase()
}

function branchFilter (currElt) {
  return currElt[3].map(elt => elt.toLowerCase()).indexOf(this.toLowerCase()) > -1
}

function classFilter (currElt) {
  let res = false
  currElt[4].forEach(elt => {
    if (elt[0].toLowerCase() === this.toLowerCase()) res = true
  })
  return res
}

function levelFilter (currElt) {
  let res = false
  currElt[4].forEach(elt => {
    if (elt[1] === this) res = true
  })
  return res
}

</script>
