import Vue from 'vue'
import { MdButton, MdContent, MdTabs } from 'vue-material/dist/components'
import 'vue-material/dist/vue-material.min.css'

Vue.use(MdButton)
Vue.use(MdContent)
Vue.use(MdTabs)

<!--/////////////////////////////////////////////
//                                             //
// Edit & Design by White Bear (@howaitokuma). //
// Raihan Hafiizh Qurratu'Ain                  //
//                                             //
///////////////////////////////////////////////// -->

<template>
  <div class="menu">
    <md-menu md-direction="bottom-start">
      <md-button md-menu-trigger><a href="#">Home</a></md-button>
    </md-menu>

    <md-menu md-direction="bottom-end">
      <md-button md-menu-trigger><a href="https://raihanhafis8.github.io/MyHome.html" target="_blank">My PortFolio</a></md-button>
    </md-menu>

  </div>
</template>

<script>
  export default {
    name: 'Directions'
  }
</script>

<style lang="scss" scoped>

  .menu{
    text-align: center;
  }

  .md-menu {
    margin: 24px;
  }

  a{
    text-decoration: none;
  }
</style>