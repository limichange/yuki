<template>
  <div id="app">
    <yuki-draggable v-for="item in items" :value="item">
      <div v-text="item.message"></div>
    </yuki-draggable>
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
      items: [{
        message: 'test1',
        top: 100,
        left: 100,
        width: 100,
        height: 100,
        index: 1
      }, {
        message: 'test2',
        top: 240,
        left: 240,
        width: 100,
        height: 100,
        index: 3
      }, {
        message: 'test3',
        top: 240,
        left: 100,
        width: 100,
        height: 100,
        index: 5
      }]
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
