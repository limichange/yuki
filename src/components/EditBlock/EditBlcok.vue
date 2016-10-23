<template>
  <div class="editBlock"
       @mousedown="mousedown"
       @mouseup="mouseup">
    <div class="content">
      <slot></slot>
    </div>
    <c-draggable :value="v"></c-draggable>
    <c-resizable :value="v"></c-resizable>
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
    mounted () {
      var self = this
      self.$on('mousemove', self.mousemove)
      self._updatePosition(self.v)
      self._updateSize(self.v)
    },
    methods: {
      mousemove (e) {
        var self = this
        self.broadcast(CDraggable.componentName, 'mousemove', e)
        this._updatePosition(this)
      },
      mouseup (e) {
        console.log('EditBlock - mouseup')
        this.broadcast(CDraggable.componentName, 'mouseup', e)
      },
      mousedown (e) {
        this.broadcast(CDraggable.componentName, 'mousedown', e)
        this._updatePosition(this)
      },
      _updatePosition ({ left, top }) {
        var self = this
        self.$el.style.left = `${parseInt(left)}px`
        self.$el.style.top = `${parseInt(top)}px`
      },
      _updateSize ({ width, height }) {
        var self = this
        self.$el.style.height = `${parseInt(height)}px`
        self.$el.style.width = `${parseInt(width)}px`
      }
    }
  }
</script>

<style lang="scss" scoped>
  .editBlock {
    position: absolute;

    .content {
      width: 100%;
      height: 100%;
      position: absolute;
    }
  }
</style>