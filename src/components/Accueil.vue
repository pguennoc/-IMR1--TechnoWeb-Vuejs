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
        <div class="box box-solid">
            <div class="box-header with-border">
              <i class="fa fa-info"></i>
              <h3 class="box-title">Description</h3>
            </div>
            <!-- /.box-header -->
            <div class="box-body">
              <dl>
                <dt>Onglet Statistiques</dt>
                <dd>Nombre de livres, nombre de sorts et nombre de sorts par livres.</dd>
                <dt>Onglet configuration</dt>
                <dd>Édition de la configuration pour la recherche des sorts.</dd>
                <dt>Onglet Recherche</dt>
                <dd>Permet de rechercher un sort et d'avoir une explication une fois le sort trouvé.</dd>
              </dl>
            </div>
            <!-- /.box-body -->
          </div>
      </section>
      <!-- /.content -->
    </div>
    <!-- /.container -->
</template>

<script>
export default {
  name: 'Accueil',
  data () {
    return {
      Onglet: 'Accueil'
    }
  }
}
</script>
