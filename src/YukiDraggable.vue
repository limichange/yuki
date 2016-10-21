<template>
  <div @mousedown="mousedown"
       @mouseup="mouseup"
       @mousemove.stop="mousemove"
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
    data () {
      return {
        isDragging: false,
        left: 0,
        top: 0,
        currentX: 0,
        currentY: 0,
        lastX: 0,
        lastY: 0
      }
    },
    methods: {
      mousedown (event) {
        var self = this
        self.isDragging = true
        var e = event
        self.currentX = e.clientX
        self.currentY = e.clientY
        event.target.classList.add('draging')
      },
      mousemove (event) {
        if (this.isDragging) {
          var e = event
          var nowX = e.clientX
          var nowY = e.clientY
          var disX = nowX - this.currentX
          var disY = nowY - this.currentY
          this.$el.style.left = parseInt(this.left) + disX + 'px'
          this.$el.style.top = parseInt(this.top) + disY + 'px'
          this.lastX = this.left + disX
          this.lastY = this.top + disY
        }
      },
      mouseup (event) {
        this.isDragging = false
        this.$el.style.left = this.lastX + 'px'
        this.$el.style.top = this.lastY + 'px'
        this.left = this.lastX
        this.top = this.lastY

        event.target.classList.remove('draging')
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
    background: blue;
    border-radius: $point-width;

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
    left: 0;
    top: 0;
    width: 100px;
    height: 100px;
    position: absolute;
    background: #00A1CA;
  }
</style>