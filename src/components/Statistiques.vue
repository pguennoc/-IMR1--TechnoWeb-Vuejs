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
        <div class="col-md-4">
          <div class="info-box bg-green">
            <span class="info-box-icon"><i class="fas fa-magic"></i></span>

            <div class="info-box-content">
              <span class="info-box-text">Nombre de sorts:</span>
              <span class="info-box-number">{{ nbSpells }}</span>
            </div>
            <!-- /.info-box-content -->
          </div>
          <!-- /.info-box -->
          <div class="info-box bg-blue">
            <span class="info-box-icon"><i class="fas fa-book"></i></span>

            <div class="info-box-content">
              <span class="info-box-text">Nombre de livres :</span>
              <span class="info-box-number">{{ nbBooks }}</span>
            </div>
            <!-- /.info-box-content -->
          </div>
          <!-- /.info-box -->
        </div>
        <div class="col-md-8">
          <div class="box">
            <div class="box-header">
              <h3 class="box-title">Nombres de sorts par livre</h3>
            </div>
            <!-- /.box-header -->
            <div class="box-body no-padding">
              <table class="table table-striped">
                <tbody>
                <tr>
                  <th style="width: 10px">#</th>
                  <th>Livre</th>
                  <th>Nombre de sorts</th>
                </tr>
                <tr v-for="(books, index) in spellsPerBooks" :key="index">
                  <td>{{ index }}.</td>
                  <td>{{ books[0] }}</td>
                  <td>{{ books[1] }}</td>
                </tr>
                </tbody>
              </table>
            </div>
            <!-- /.box-body -->
          </div>
        </div>
      </section>
      <!-- /.content -->
    </div>
    <!-- /.container -->
</template>

<script>
export default {
  name: 'Statistiques',
  data () {
    return {
      Onglet: 'Statistiques',
      data: [],
      nbBooks: 0,
      nbSpells: 0,
      spellsPerBooks: 0
    }
  },
  created () {
    this.data = sortTable
    this.nbBooks = this.getNbBooks()
    this.nbSpells = this.getNbSpells()
    this.spellsPerBooks = this.getNbSpellsPerBooks()
  },
  methods: {
    getNbBooks () {
      var cpt = 0
      var titles = []
      for (let i = 0; i < this.data.length; i++) {
        if (!titles.includes(this.data[i][0])) {
          titles.push(this.data[i][0])
          cpt++
        }
      }
      return cpt
    },
    getNbSpells () {
      return this.data.length
    },
    getNbSpellsPerBooks () {
      var res = new Map()
      for (let i = 0; i < this.data.length; i++) {
        if (res.get(this.data[i][0]) !== undefined) {
          res.set(this.data[i][0], res.get(this.data[i][0]) + 1)
        } else {
          res.set(this.data[i][0], 1)
        }
      }
      return res
    }
  }
}
</script>
