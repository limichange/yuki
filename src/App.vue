<template>
  <div id="app">
    <c-edit-area></c-edit-area>
  </div>
</template>

<script>
import CEditArea from './components/EditArea'

export default {
  name: 'app',
  components: {
    CEditArea
  },
  data: function () {
    return {
      version: '0.0.1'
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin: 0 auto;
  position: relative;
}
</style>
