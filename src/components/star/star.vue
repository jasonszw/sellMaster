<template>
  <div class="star" :class="starType">
    <span class="starItem" v-for="itemClass in itemClasses" :class="itemClass"></span>
  </div>
</template>

<script type="text/javascript">
  const LENGTH = 5;
  const CLS_ON = 'on';
  const CLS_OFF = 'off';
  const CLS_HALF = 'half';
  export default {
    props: {
      size: {
        type: Number
      },
      score: {
        type: Number
      }
    },
    computed: {
      starType: function () {
        return 'star' + this.size;
      },
      itemClasses: function () {
        let result = [];
        let score = Math.floor(this.score * 2) / 2;
        let hasDecimal = score % 1 !== 0;
        let integer = Math.floor(score);
        for (let i = 0; i < integer; i++) {
          result.push(CLS_ON);
        }
        if (hasDecimal) {
          result.push(CLS_HALF);
        }
        while (result.length < LENGTH) {
          result.push(CLS_OFF);
        }
        return result;
      }
    }
  };
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="less">
  @import "../../assets/less/mixin";
  .star {
    .starItem {
      display: inline-block;
    }
    &.star48 {
      .starItem {
        width: 20px;
        height: 20px;
        margin-right: 22px;
        &.on {
          .bgImg(star48_on);
        }
        &.off {
          .bgImg(star48_off);
        }
        &.half {
          .bgImg(star48_half);
        }
        &:last-child {
          margin-right: 0px;
        }
      }
    }
    &.star36 {
      .starItem {
        width: 15px;
        height: 15px;
        margin-right: 6px;
        &.on {
          .bgImg(star36_on);
        }
        &.off {
          .bgImg(star36_off);
        }
        &.half {
          .bgImg(star36_half);
        }
        &:last-child {
          margin-right: 0px;
        }
      }
    }
    &.star24 {
      .starItem {
        width: 10px;
        height: 10px;
        margin-right: 3px;
        &.on {
          .bgImg(star24_on);
        }
        &.off {
          .bgImg(star24_off);
        }
        &.half {
          .bgImg(star24_half);
        }
        &:last-child {
          margin-right: 0px;
        }
      }
    }
  }

</style>
