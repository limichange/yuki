<template>
  <div @mousedown="mousedown"
       @mouseup="mouseup"
       @mousemove="mousemove"
       @mouseover="mouseover"
       class="main-div">
    <slot></slot>

    <div class="line left"></div>
    <div class="line right"></div>
    <div class="line top"></div>
    <div class="line bottom"></div>

    <point v-for="point in points" v-show="isSelected" v-bind:value="point"></point>
  </div>
</template>

<script>
  import Point from './Point.vue'

  export default {
    name: 'CDraggable',
    componentName: 'draggable',
    props: ['value'],
    data () {
      return {
        points: [
          ['left', 'top'],
          ['top', 'center'],
          ['right', 'top'],
          ['left', 'middle'],
          ['right', 'middle'],
          ['left', 'bottom'],
          ['center', 'bottom'],
          ['right', 'bottom'],
          ['center', 'out']
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
      Point
    },
    mounted () {
      var self = this
      self._updatePosition(self.v)
      self._updateSize(self.v)
    },
    methods: {
      mouseover (e) {
        this._dragEnd(e)
      },
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
            left: self.v.left + disX,
            top: self.v.top + disY
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
  $line-width: 1px;

  .line {
    background: #000;
    position: absolute;

    &.out {

    }
    &.top {
      left: 0;
      top: 0;
      width: 100%;
      height: $line-width;
    }
    &.right {
      right: 0;
      top: 0;
      width: $line-width;
      height: 100%;
    }
    &.left {
      left: 0;
      top: 0;
      width: $line-width;
      height: 100%;
    }
    &.bottom {
      left: 0;
      bottom: 0;
      width: 100%;
      height: $line-width;
    }
  }

  .main-div {
    position: absolute;
    background: #00A1CA;
  }
</style>