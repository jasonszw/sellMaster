<template>
    <div class="shopcart">
      <div class="content">
        <div class="contentLeft">
          <div class="logoWraper">
            <div class="logo">
              <span class="iconShopping_cart"></span>
            </div>
          </div>
          <div class="price">￥0</div>
          <div class="desc">另需配送费￥{{deliveryPrice}}元</div>
        </div>
        <div class="contentRight">￥{{minPrice}}起送</div>
      </div>
    </div>
</template>

<script>
    export default {
      props: {
        deliveryPrice: {
          type: Number,
          default: 0
        },
        minPrice: {
          type: Number,
          default: 0
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
          span {
            display: inline-block;
            line-height: 44px;
            font-size: 24px;
            color: #80858a;
          }
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
      }
      .desc {
        padding-left: 6px;
      }
    }
    .contentRight {
      flex: 0 0 105px;
      width: 105px;
      background: rgb(44, 51, 58);
      text-align: center;
      vertical-align: top;
      line-height: 48px;
      font-size: 12px;
      font-weight: 700;
    }
  }
</style>
