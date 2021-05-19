<template>
  <div class="container">
    <h1 class="title">Can I Text 911?</h1>
    <h2 class="subtitle">Search your county in the table to find out</h2>
    <datatable/>
  </div>
</template>

<script>
import Datatable from "./components/datatable";

export default {
  name: 'App',
  components: {
    Datatable
  }
}
</script>
