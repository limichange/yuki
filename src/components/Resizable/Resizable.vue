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
      }
    }
  }
</script>

<style lang="scss" scoped>
  .resizable {
    width: 100%;
    height: 100%;
    position: absolute;
  }
</style>
