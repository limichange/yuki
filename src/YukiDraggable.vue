<template>
  <div @mousedown="mousedown"
       @mouseup="mouseup"
       @mousemove="mousemove"
       class="main">
    <slot></slot>
  </div>
</template>

<script>
  export default {
    name: 'YukiDraggable',
    data () {
      return {

      }
    },
    methods: {
      mousedown () {
        console.log('mousedown')
      },
      mousemove () {
        console.log('mousemove')
      },
      mouseup () {
        console.log('mouseup')
      }
    }
  }
</script>

<style scoped>
  .main {
    background: #A47D29;
    position: absolute;
    left: 0;
    top: 0;
    width: 200px;
    height: 200px;
  }
</style>