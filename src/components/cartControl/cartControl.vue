<template>
  <div class="cartControl">
    <div class="cartDecrease iconRemove_circle_outline" v-show="food.count>0"></div>
    <div class="cartContent" v-show="food.count>0">{{food.count}}</div>
    <div class="cartAdd iconAdd_circle" @click="cartAdd"></div>
  </div>
</template>

<script>
  export default {
    props: {
      food: {
        type: Object
      }
    },
    methods: {
      cartAdd () {
        console.log(11);
      }
    }
  };
</script>

<style lang="less" scoped>
  .cartControl {
    font-size: 0;
    position: relative;
    bottom: 24px;
    .cartDecrease, .cartAdd {
      display: inline-block;
      line-height: 24px;
      font-size: 24px;
      padding: 6px;
      color: rgb(0, 160, 220);
    }
    .cartDecrease {
      display: inline-block;
    }
    .cartContent {
      display: inline-block;
    }
    .cartAdd {
      display: inline-block;
    }
  }
</style>
