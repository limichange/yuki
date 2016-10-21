<template>
  <div @mousedown="mousedown"
       @mouseup="mouseup"
       @mousemove="mousemove"
       v-bind:style="styleObject"
       class="main-div">
    <slot></slot>
  </div>
</template>

<script>
  export default {
    name: 'YukiDraggable',
    data () {
      return {
        styleObject: {
          position: 'absolute',
          width: '100px',
          height: '100px',
          left: '100px',
          top: '100px',
          background: '#eeeeee'
        }
      }
    },

    methods: {
      mousedown (event) {
        console.log('mousedown')
      },
      mousemove (event) {
        this._generatePosition(event)
        console.log('mousemove')
      },
      mouseup (event) {
        console.log('mouseup')
      },
      _generatePosition (event) {
        var pageX = event.pageX
        var pageY = event.pageY

        console.log(pageX, pageY)
      }
    }
  }
</script>

<style scoped>
  .main-div {

  }
</style>