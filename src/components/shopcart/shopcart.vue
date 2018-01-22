<template>
    <div class="shopcart">
      <div class="content">
        <div class="contentLeft">
          <div class="logoWraper">
            <div class="logo">
              <span class="iconShopping_cart"></span>
            </div>
          </div>
          <div class="price"></div>
          <div class="drsc"></div>
        </div>
        <div class="contentRight"></div>
      </div>
    </div>
</template>

<script>
    export default {
        name: 'shopcart'
    };
</script>

<style lang="less" scoped>
  @import "../../assets/less/icon.less";
  .shopcart {
    position: fixed;
    left: 0;
    bottom: 0;
    width: 100%;
    height: 48px;
    z-index: 10;
  }
</style>
