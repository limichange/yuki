<template>
  <div class="editArea"
       @mousemove="mousemove"
       @mouseup="mouseup"
       @mousedown="mousedown">
    <div>x: {{mouseX}}</div>
    <div>y: {{mouseY}}</div>
    <slot></slot>
  </div>
</template>

<script>
  import emitter from '../mixins/emitter'
  import _ from 'lodash'
  import CDraggable from '../Draggable'

  export default {
    name: 'EditArea',
    componentName: 'EditArea',
    mixins: [emitter],
    data () {
      return {
        mouseX: 0,
        mouseY: 0
      }
    },
    methods: {
      mousemove: _.throttle(function (e) {
        var self = this
        self.mouseX = e.clientX
        self.mouseY = e.clientY
        self.broadcast(CDraggable.componentName, 'mousemove', e)
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
    width: 960px;
    height: 460px;
    background: #eeeeee;
  }
</style>