<template>
  <div class="line">

  </div>
</template>

<script>
  export default {
    name: 'Line',
    props: ['value'],
    mounted () {
      this.$el.classList.add(this.value[0])
    },
    data: function () {
      return {}
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
</style>
