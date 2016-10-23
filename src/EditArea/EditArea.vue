<template>
  <div class="editArea" @mousemove="mousemove">
    <div>{{mouseX}}, {{mouseY}}</div>
    <slot></slot>
  </div>
</template>

<script>
  import _ from 'lodash'

  export default {
    name: 'EditArea',
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
      }, 15)
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