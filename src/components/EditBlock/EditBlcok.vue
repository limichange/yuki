<template>
  <div class="editBlock">
    <!-- <c-draggable :value="item"></c-draggable> -->
    <!-- <c-resizable :value="item"></c-resizable> -->
    <div v-text="v.message"></div>
  </div>
</template>

<script>
  import emitter from '../../mixins/emitter'
  import CDraggable from '../Draggable'
  import CResizable from '../Resizable'

  export default {
    name: 'EditBlock',
    componentName: 'CEditBlock',
    mixins: [emitter],
    components: {
      CDraggable,
      CResizable
    },
    props: ['value'],
    data () {
      return {
        v: this.value
      }
    },
    methods: {
      mousemove () {

      },
      mouseup () {

      },
      mousedown () {

      }
    }
  }
</script>

<style lang="scss" scoped>
  .editBlock {
    position: absolute;
  }
</style>