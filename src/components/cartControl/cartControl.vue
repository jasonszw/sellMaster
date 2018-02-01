<template>
  <div class="cartControl">
    <transition name="move">
      <div class="cartDecrease iconRemove_circle_outline" v-show="food.count>0" @click="cartRemove"></div>
    </transition>
    <div class="cartContent" v-show="food.count>0">{{food.count}}</div>
    <div class="cartAdd iconAdd_circle" @click="cartAdd"></div>
  </div>
</template>

<script>
  import Vue from 'vue';
  export default {
    props: {
      food: {
        type: Object
      }
    },
    methods: {
      // 添加商品
      // 添加商品
      cartAdd () {
        if (!this.food.count) {
          Vue.set(this.food, 'count', 1);
        } else {
          this.food.count++;
        }
      },
      // 删除商品
      cartRemove () {
        if (this.food.count) {
          this.food.count--;
        }
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
      padding: 6px;
      line-height: 24px;
      font-size: 24px;
      color: rgb(0, 160, 220);
    }
    .cartDecrease {
      transition: all 0.2s linear;
      &.move-enter, &.move-leave-to {
        transform: translate(24px, 0) rotate(180deg);
        opacity: 0;
      }
    }
    .cartContent {
      display: inline-block;
      vertical-align: top;
      width: 12px;
      padding-top: 6px;
      text-align: center;
      font-size: 10px;
      color: rgb(147, 153, 159);
      line-height: 24px;
    }
    .cartAdd {
      display: inline-block;
    }
  }
</style>
