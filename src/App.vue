<template>
  <div id="app">
    <yuki-draggable>test</yuki-draggable>
  </div>
</template>

<script>
import YukiDraggable from './YukiDraggable.vue'

export default {
  name: 'app',
  components: {
    YukiDraggable
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
