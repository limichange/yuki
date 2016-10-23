<template>
  <div class="resizable"
       @mousedown="mousedown">
    <slot></slot>
    <c-line v-for="line in lines" v-show="isSelected" :value="line"></c-line>
    <c-point v-for="point in points" v-show="isSelected" :value="point"></c-point>
  </div>
</template>

<script>
  import CPoint from './Point.vue'
  import CLine from './Line.vue'

  export default {
    name: 'Resizable',
    componentName: 'CResizable',
    props: ['value'],
    components: {
      CPoint,
      CLine
    },
    mounted () {
      var self = this
      self._updatePosition(self.v)
      self._updateSize(self.v)
    },
    data: function () {
      return {
        isSelected: true,
        v: this.value,
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
        ]
      }
    },
    methods: {
      mousedown () {
        console.log('mousedown')
        this.isSelected = true
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
  .resizable {
    position: absolute;
  }
</style>
