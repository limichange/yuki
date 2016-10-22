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

    <div class="point left top"></div>
    <div class="point top center"></div>
    <div class="point right top"></div>
    <div class="point left middle"></div>
    <div class="point right middle"></div>
    <div class="point left bottom"></div>
    <div class="point center bottom"></div>
    <div class="point right bottom"></div>
    <div class="point center out"></div>
  </div>
</template>

<script>
  export default {
    name: 'YukiDraggable',
    props: ['value'],
    data () {
      return {
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
      self._updatePosition(self.v)
      self._updateSize(self.v)
    },
    methods: {
      mouseover (e) {
        this._dragEnd(e)
      },
      mousedown (e) {
        var self = this
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

  $point-width: 10px;
  $point-height: 10px;

  $point-width-half: $point-width / 2;
  $point-height-half: $point-height / 2;

  .point {
    position: absolute;
    width: $point-width;
    height: $point-height;
    background: white;
    border-radius: $point-width;
    border: 1px solid black;
    box-sizing: border-box;

    &.out {
      background: green;
      top: -30px;
    }
    &.top {
      top: - $point-height-half;
    }
    &.bottom {
      bottom: - $point-height-half;
    }
    &.left {
      left: - $point-width-half;
    }
    &.right {
      right: - $point-width-half;
    }
    &.middle {
      top: 50%;
      margin-top: - $point-height-half;
    }
    &.center {
      left: 50%;
      margin-left: - $point-width-half;
    }
  }

  .main-div {
    width: 100px;
    height: 100px;
    position: absolute;
    background: #00A1CA;
  }
</style>