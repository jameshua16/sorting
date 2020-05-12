<template>
  <div id="app">
    <Nav/>
    <Sort/>
  </div>
</template>

<script>
import Sort from './components/Sort.vue'
import Nav from './components/Nav.vue'

export default {
  name: 'App',
  components: {
    Sort,Nav
  }
}
</script>

<style>
.app{
  position: relative;
}
</style>
