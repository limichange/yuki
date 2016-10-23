<template>
  <div id="app">
    <c-draggable v-for="item in items" :value="item">
      <div v-text="item.message"></div>
    </c-draggable>
  </div>
</template>

<script>
import CDraggable from './Draggable'

export default {
  name: 'app',
  components: {
    CDraggable
  },
  data: function () {
    return {
      items: [{
        message: 'test1',
        top: 100,
        left: 100,
        width: 150,
        height: 100,
        index: 1,
        background: '#eeeeee'
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
