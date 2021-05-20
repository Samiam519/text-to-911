<template>
  <div id="vue-container">
    <div class="container p-4" id="wrapper">
      <h1 class="title">Can I Text 911?</h1>
      <h2 class="subtitle">Search your county in the table to find out what methods of reaching 911 are available in your area.</h2>
      <datatable :isMobile="isMobile"/>
    </div>
    <footer class="footer p-4">
      <div class="content is-flex is-justify-content-space-between" v-bind:class="{ 'is-flex-direction-column': isMobile }">
        <div>
          Made with <b-icon icon="heart"></b-icon> by <a href="https://www.github.com/Samiam519/" target="_blank">Sam</a>.
        </div>
        <div>
          Source: <a href="https://www.fcc.gov/file/12285/download" target="_blank">FCC PSAP Registry</a>. <br v-if="isMobile">Last Updated: May 2021
        </div>
      </div>
    </footer>
  </div>
</template>

<script>
import Datatable from "./components/datatable";

export default {
  name: 'App',
  components: {
    Datatable
  },
  data(){
    return {
      isMobile: screen.width <= 750
    }
  }
}
</script>
