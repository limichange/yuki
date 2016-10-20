<template>
  <div class="main">
    <slot></slot>
  </div>
</template>

<script>
  export default {
    name: 'YukiDraggable',
    data () {
      return {

      }
    }
  }
</script>

<style scoped>
  .main {
    background: red;
    position: absolute;
    left: 0;
    top: 0;
  }
</style>