<template>
  <div id="app">
    <c-edit-area>
      <c-draggable v-for="item in items" :value="item">
        <div v-text="item.message"></div>
      </c-draggable>
    </c-edit-area>
  </div>
</template>

<script>
import CDraggable from './Draggable'
import CEditArea from './EditArea'

export default {
  name: 'app',
  components: {
    CDraggable,
    CEditArea
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
        width: 70,
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
  margin: 0 auto;
  position: relative;
}
</style>
