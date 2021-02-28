<template>
  <div id="app">
    <div class="wrapper">
    <header class="main-header">
    <nav class="navbar navbar-static-top">
      <div class="container">
        <div class="navbar-header">
          <a class="navbar-brand"><i class="fas fa-dragon"></i> <b>D</b>&<b>D</b></a>
          <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#navbar-collapse">
            <i class="fa fa-bars"></i>
          </button>
        </div>

        <!-- Collect the nav links, forms, and other content for toggling -->
        <div class="collapse navbar-collapse pull-left" id="navbar-collapse">
          <ul class="nav navbar-nav">
            <li v-for="tab in tabs" v-bind:key="tab" v-bind:class="['tab-button', { active: currentTab === tab }]" v-on:click="currentTab = tab">
              <a>{{ tab }}</a>
            </li>
          </ul>
        </div>
        <!-- /.navbar-collapse -->
      </div>
      <!-- /.container-fluid -->
    </nav>
  </header>
  <!-- Full Width Column -->
  <div class="content-wrapper">
    <component v-bind:is="currentTabComponent" class="tab"></component>
  </div>
  <!-- /.content-wrapper -->
  <footer class="main-footer">
    <div class="container">
      <div class="pull-right hidden-xs">
        <b>Version</b> 2.4.13
      </div>
      <strong>Copyright &copy; 2014-2019 <a href="https://adminlte.io">AdminLTE</a>.</strong> All rights
      reserved.
    </div>
    <!-- /.container -->
  </footer>
  </div>
<!-- ./wrapper -->
  </div>
</template>

<script>
import Accueil from './components/Accueil'
import Statistiques from './components/Statistiques'
import Recherche from './components/Recherche'
import Configuration from './components/Configuration'

export default {
  name: 'App',
  components: {
    Accueil, Configuration, Statistiques, Recherche
  },
  data () {
    return {
      currentTab: 'Accueil',
      tabs: ['Accueil', 'Statistiques', 'Configuration', 'Recherche']
    }
  },
  computed: {
    currentTabComponent: function () {
      return this.currentTab
    }
  }

}

/* global sortTable */

</script>

<style scoped>
a {
  cursor: pointer;
  text-decoration: none;
}
</style>
