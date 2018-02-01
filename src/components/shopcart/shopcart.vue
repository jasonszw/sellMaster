<template>
    <div class="shopcart">
      <div class="content">
        <div class="contentLeft">
          <div class="logoWraper">
            <div class="logo" :class="{'highLight': totalCount > 0}">
              <span class="iconShopping_cart" :class="{'highLight': totalCount > 0}"></span>
            </div>
            <div class="num" v-show="totalCount > 0">{{totalCount}}</div>
          </div>
          <div class="price" :class="{'highLight': totalPrice > 0}">￥{{totalPrice}}</div>
          <div class="desc">另需配送费￥{{deliveryPrice}}元</div>
        </div>
        <div class="contentRight" :class="setCount">{{payDesc}}</div>
      </div>
    </div>
</template>

<script>
    export default {
      props: {
        selectFoods: {
          type: Array,
          default () {
            return [];
          }
        },
        deliveryPrice: {
          type: Number,
          default: 0
        },
        minPrice: {
          type: Number,
          default: 0
        }
      },
      computed: {
        // 购买商品总额
        totalPrice () {
          console.log(this.selectFoods);
          let total = 0;
          this.selectFoods.forEach(function (food) {
            total += food.price * food.count;
          });
          return total;
        },
        // 购买的商品总数
        totalCount () {
          let count = 0;
          this.selectFoods.forEach(function (food) {
            count += food.count;
          });
          return count;
        },
        payDesc () {
          if (this.totalPrice === 0) {
            return `￥${this.minPrice}起送`;
          } else if (this.totalPrice < this.minPrice) {
            let diff = this.minPrice - this.totalPrice;
            return `还差￥${diff}元起送`;
          } else {
            return '去结算';
          }
        },
        setCount () {
          if (this.totalPrice < this.minPrice) {
            return 'not-enough';
          } else {
            return 'enough';
          }
        }
      }
    };
</script>

<style lang="less" scoped>
  .shopcart {
    position: fixed;
    left: 0;
    bottom: 0;
    width: 100%;
    height: 48px;
    z-index: 10;
    .content {
      display: flex;
      height: 100%;
      color: rgba(255,255,255,0.4);
    }
    .contentLeft {
      background: #141d27;
      flex: 1;
      font-size: 0px;
      .logoWraper {
        display: inline-block;
        width: 56px;
        height: 56px;
        border-radius: 50%;
        position: relative;
        top: -10px;
        margin: 0 6px;
        background: #141d27;
        .logo {
          width: 44px;
          height: 44px;
          border-radius: 50%;
          background: rgb(44, 51, 58);
          margin: 6px;
          text-align: center;
          &.highLight {
            background: rgb(26, 160, 217);
          }
          span {
            display: inline-block;
            line-height: 44px;
            font-size: 24px;
            color: #80858a;
            &.highLight {
              color: #fff;
            }
          }
        }
        .num {
          position: absolute;
          top: 0;
          right:0;
          width: 24px;
          height: 16px;
          line-height: 16px;
          text-align: center;
          border-radius: 16px;
          font-size: 9px;
          font-weight: 700;
          color: #fff;
          background: rgb(240, 20, 20);
          box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.4);
        }
      }
      .price,.desc {
        display: inline-block;
        vertical-align: top;
        font-weight: 700;
        font-size: 12px;
        margin-top: 19px;
      }
      .price {
        padding-right: 6px;
        border-right: 1px solid rgba(255,255,255,0.1);
        &.highLight {
          color: #fff;
        }
      }
      .desc {
        padding-left: 6px;
      }
    }
    .contentRight {
      flex: 0 0 105px;
      width: 105px;
      text-align: center;
      vertical-align: top;
      line-height: 48px;
      font-size: 12px;
      font-weight: 700;
      &.not-enough {
        background: rgb(44, 51, 58);
      }
      &.enough {
        background: #00b43c;
        color: #fff;
      }
    }
  }
</style>
