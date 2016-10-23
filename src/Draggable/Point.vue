<template>
  <div class="point"
       @mouseup="mouseup"
       @mousemove="mousemove"
       @mousedown="mousedown">
  </div>
</template>

<script>
  export default {
    name: 'Point',
    props: ['value'],
    data: function () {
      return {
        isDragging: false
      }
    },
    mounted () {
      this.$el.classList.add(this.value.position[0])
      this.$el.classList.add(this.value.position[1])
    },
    methods: {
      mousemove (e) {
        var self = this
        if (self.isDragging) {

        }
      },
      mouseup (e) {
        var self = this
        self.isDragging = false
      },
      mousedown (e) {
        var self = this
        self.isDragging = true
        self.currentX = e.clientX
        self.currentY = e.clientY
      }
    }
  }
</script>

<style lang="scss" scoped>
  $point-width: 8px;
  $point-height: $point-width;

  $point-width-half: $point-width / 2;
  $point-height-half: $point-height / 2;

  .point {
    position: absolute;
    width: $point-width;
    height: $point-height;
    background: white;
    border: 1px solid black;
    box-sizing: border-box;

    &.out {
      border-radius: $point-width;
      background: #2FBA22;
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
      cursor: ew-resize;
      top: 50%;
      margin-top: - $point-height-half;
    }
    &.center {
      cursor: ns-resize;
      left: 50%;
      margin-left: - $point-width-half;
    }
  }
</style>
