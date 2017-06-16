<template>
    <div class="star" :class="starType">
      <span class="star-item" v-for="itemClass in itemClasses" :class="itemClass" track-by="$index"></span>
      {{itemClasses}}
    </div>
</template>
<style lang="stylus" rel="stylesheet/stylus" type="text/css">
  @import "../../common/stylus/mixin.styl"
  .star
    font-size 0;
    .star-item
      display: inline-block;
      background-repeat no-repeat;
    &.star-48
      .star-item
        width 20px;
        height 20px;
        margin-right 22px;
        background-size 20px 20px;
        &.last-child
          margin-right 0;
        &.on
          bg-img('star48_on')
        &.half
          bg-img('star48_half')
        &.off
          bg-img('star48_off')
    &.star-36
      .star-item
        width 15px;
        height 15px;
        margin-right 16px;
        background-size 15px 15px;
        &.last-child
          margin-right 0;
        &.on
          bg-img('star36_on')
        &.half
          bg-img('star36_half')
        &.off
          bg-img('star36_off')
    &.star-24
      .star-item
        width 10px;
        height 10px;
        margin-right 3px;
        background-size 10px 10px;
        &.last-child
          margin-right 0;
        &.on
          bg-img('star24_on')
        &.half
          bg-img('star24_half')
        &.off
          bg-img('star24_off')
</style>
<script type="text/ecmascript-6">
    const Length = 5;
    const clsOn = 'on';
    const clsHalf = 'half';
    const clsOff = 'off';
    export default {
      // 定义组件的属性
      props: {
        size: {
          type: Number
        },
        score: {
          type: Number
        }
      },
      // 组件的计算属性
      computed: {
        starType () {
          return 'star-' + this.size;
        },
        itemClasses () {
          let result = [];
          // 向下取整Math.floor
          let score = Math.floor(this.score * 2) / 2;
          // 对1取余，判断是否为小数
          let hasDecimal = score % 1 !== 0;
          let integer = Math.floor(score);
          for (let i = 0; i < integer; i++) {
            result.push(clsOn);
          };
          if (hasDecimal) {
            result.push(clsHalf);
          };
          while (result.length < Length) {
            result.push(clsOff);
          };
          return result;
        }
      }
    };
</script>
