<template>
  <div class="editArea"
       @mousemove="mousemove"
       @mouseup="mouseup"
       @mousedown="mousedown">
    <c-edit-block v-for="item in items" :value="item"></c-edit-block>

    <div class="info-panel">
      <div>x: {{mouseX}} y: {{mouseY}}</div>
    </div>
  </div>
</template>

<script>
  import _ from 'lodash'
  import emitter from '../../mixins/emitter'
  import CEditBlock from '../EditBlock'

  export default {
    name: 'EditArea',
    componentName: 'CEditArea',
    mixins: [emitter],
    components: {
      CEditBlock
    },
    data () {
      return {
        v: this.value,
        mouseX: 0,
        mouseY: 0,
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
    },
    methods: {
      mousemove: _.throttle(function (e) {
        var self = this
        self.mouseX = e.clientX
        self.mouseY = e.clientY
        self.broadcast(CEditBlock.componentName, 'mousemove', e)
      }, 15),
      mouseup () {

      },
      mousedown () {

      }
    }
  }
</script>

<style lang="scss" scoped>
  .editArea {
    position: relative;
    width: 100%;
    height: 460px;
    background: #eeeeee;
  }

  .info-panel {
    position: absolute;
    display: flex;
    right: 0;
    bottom: 0;
  }
</style>