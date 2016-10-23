<template>
  <div @mousedown="mousedown"
       @mouseup="mouseup"
       class="draggable">
    <div>{{lastX}}, {{lastY}}</div>
    <slot></slot>

    <c-line v-for="line in lines" v-show="isSelected" :value="line"></c-line>
    <c-point v-for="point in points" v-show="isSelected" :value="point"></c-point>
  </div>
</template>

<script>
  import emitter from '../mixins/emitter'
  import CPoint from './Point.vue'
  import CLine from './Line.vue'

  export default {
    name: 'Draggable',
    componentName: 'Draggable',
    mixins: [emitter],
    props: ['value'],
    data () {
      return {
        lines: [
          ['top'],
          ['bottom'],
          ['left'],
          ['right']
        ],
        points: [
          {position: ['left', 'top']},
          {position: ['top', 'center']},
          {position: ['right', 'top']},
          {position: ['left', 'middle']},
          {position: ['right', 'middle']},
          {position: ['left', 'bottom']},
          {position: ['center', 'bottom']},
          {position: ['right', 'bottom']},
          {position: ['center', 'out']}
        ],
        isSelected: false,
        isDragging: false,
        currentX: 0,
        currentY: 0,
        v: this.value,
        lastX: this.value.left,
        lastY: this.value.top
      }
    },
    components: {
      CPoint,
      CLine
    },
    mounted () {
      var self = this
      self._updatePosition(self.v)
      self._updateSize(self.v)
      self.$on('mousemove', self.mousemove)
    },
    methods: {
      mousedown (e) {
        var self = this
        self.isSelected = true
        self.isDragging = true
        self.currentX = e.clientX
        self.currentY = e.clientY
        e.target.classList.add('draging')
      },
      mousemove (e) {
        if (this.isDragging) {
          var self = this
          var nowX = e.clientX
          var nowY = e.clientY
          var disX = nowX - self.currentX
          var disY = nowY - self.currentY
          self.lastX = self.v.left + disX
          self.lastY = self.v.top + disY

          self._updatePosition({
            left: self.lastX,
            top: self.lastY
          })
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
        self._updatePosition(self)
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
    user-select: none;
    position: absolute;
    background: #00A1CA;
  }
</style>