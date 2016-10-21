<template>
  <div @mousedown="mousedown"
       @mouseup="mouseup"
       @mousemove="mousemove"
       v-bind:style="styleObject"
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
        styleObject: {
          position: 'absolute',
          width: '100px',
          height: '100px',
          left: '100px',
          top: '100px',
          background: '#00A1CA'
        }
      }
    },
    methods: {
      mousedown (event) {
        console.log('mousedown')
        event.target.classList.add('draging')
      },
      mousemove (event) {
        this._generatePosition(event)
        console.log('mousemove')
      },
      mouseup (event) {
        console.log('mouseup')
        event.target.classList.remove('draging')
      },
      _generatePosition (event) {
        var pageX = event.pageX
        var pageY = event.pageY

        console.log(pageX, pageY)
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

  }
</style>