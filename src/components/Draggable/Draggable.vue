<template>
  <div @mousedown="mousedown"
       @mouseup="mouseup"
       class="draggable">
    <slot></slot>
  </div>
</template>

<script>
  import emitter from '../../mixins/emitter'

  export default {
    name: 'Draggable',
    componentName: 'CDraggable',
    mixins: [emitter],
    props: ['value'],
    data () {
      return {
        isSelected: false,
        isDragging: false,
        currentX: 0,
        currentY: 0,
        v: this.value,
        lastX: this.value.left,
        lastY: this.value.top
      }
    },
    mounted () {
      var self = this
      self.$on('mousemove', self.mousemove)
      self.$on('mousedown', self.mousedown)
      self.$on('mouseup', self.mouseup)
    },
    methods: {
      mousedown (e) {
        console.log(e)
        var self = this
        self.isSelected = true
        self.isDragging = true
        self.currentX = e.clientX
        self.currentY = e.clientY
      },
      mousemove (e) {
        console.log(e)
        if (this.isDragging) {
          var self = this
          var nowX = e.clientX
          var nowY = e.clientY
          var disX = nowX - self.currentX
          var disY = nowY - self.currentY
          self.lastX = self.v.left + disX
          self.lastY = self.v.top + disY

          // self._updatePosition({
          //   left: self.lastX,
          //   top: self.lastY
          // })
        }
      },
      mouseup (e) {
        this._dragEnd(e)
      },
      _dragEnd (e) {
        var self = this
        self.isDragging = false
        self.v.left = self.lastX
        self.v.top = self.lastY
        // self._updatePosition(self)
        self.$emit('input', self.v)
        e.target.classList.remove('draging')
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
  .draggable {
    width: 100%;
    height: 100%;
    user-select: none;
    position: absolute;
    background: #00A1CA;
    opacity: .4;
  }
</style>