<template>
  <div id="app">
    <yuki-draggable v-model="item1">test1</yuki-draggable>
    <yuki-draggable v-model="item2">test2</yuki-draggable>
  </div>
</template>

<script>
import YukiDraggable from './YukiDraggable.vue'

export default {
  name: 'app',
  components: {
    YukiDraggable
  },
  data: function () {
    return {
      item1: {
        top: 100,
        left: 100
      },
      item2: {
        top: 240,
        left: 100
      }
    }
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
