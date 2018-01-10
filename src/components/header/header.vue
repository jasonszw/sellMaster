<template>
  <div class="header">
    <div class="contentWrap">
      <div class="leftContent">
        <img height="64" width="64" :src="seller.avatar" alt="">
      </div>
      <div class="rightContent">
        <div class="title">
          <span class="brand"></span>
          <span class="name">{{seller.name}}</span>
        </div>
        <div class="description">
          {{seller.description}}/{{seller.deliveryTime}}分钟送达
        </div>
        <div class="support" v-if="seller.supports">
          <span class="icon" :class="classMap[seller.supports[0].type]"></span>
          <span class="text">{{seller.supports[0].description}}</span>
        </div>
      </div>
      <div class="count" v-if="seller.supports" @click="showDetail">
        <span class="number">{{seller.supports.length}}个</span>
        <i class="">></i>
      </div>
    </div>
    <div class="noticeWrap" @click="showDetail">
      <span class="notice"></span><span class="noticeContent">{{seller.bulletin}}</span>
      <i>></i>
    </div>
    <div class="background"><img width="100%" height="100%" :src="seller.avatar" alt=""></div>
    <div class="detail" v-if="detailShow">
      <div class="detailWrap">
        <div class="detailMain">
          <div class="detailTitle">{{seller.name}}</div>
          <star class="detailStar" :size="48" :score="seller.score"></star>
          <div class="discountMessage">
            <span class="line"></span><span class="discountTitle">优惠信息</span><span class="line"></span>
          </div>
          <div class="detailDiscountMessage">
            <div v-for="(messageItem, index) in seller.supports" class="message"><span class="messageIcon" :class="classMap[seller.supports[index].type]"></span><span class="itemMessage">{{seller.supports[index].description}}</span></div>
          </div>
          <div class="businessMessage">
            <span class="line"></span><span class="businessTitle">商家公告</span><span class="line"></span>
          </div>
          <div class="businessNotice">{{seller.bulletin}}</div>
        </div>
      </div>
      <div class="detailClose"><i @click="hideDeteail" class="iconClose"></i></div>
    </div>
  </div>
</template>

<script type="text/javascript">
  import star from '../star/star.vue';
  export default {
    data () {
      return {
        classMap: ['decrease', 'discount', 'special', 'invoice', 'guarantee'],
        detailShow: false
      };
    },
    props: {
      seller: {
        type: Object
      }
    },
    methods: {
      showDetail: function () {
        this.detailShow = true;
      },
      hideDeteail: function () {
        this.detailShow = false;
      }
    },
    created: function () {
    },
    components: {
      star
    }
  };
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="less" scoped>
  @import "../../assets/less/mixin.less";
  @import "../../assets/less/icon.less";
  .header {
    color: #fff;
    background-color: rgba(7,17,27,0.5);
    position: relative;
    overflow: hidden;
  }
  .contentWrap {
    padding: 24px 12px 18px 24px;
    overflow: hidden;
    position: relative;
    .leftContent {
      float: left;
      margin-right: 16px;
      img {
        -webkit-border-radius: 2px;
        -moz-border-radius: 2px;
        border-radius: 2px;
      }
    }
    .rightContent {
      float: left;
      .title {
        font-size: 0px;
        margin:2px 0px 8px 0px;
        .brand {
          display: inline-block;
          vertical-align: top;
          width: 30px;
          height: 18px;
          .bgImg(brand);
        }
        .name {
          margin-left: 6px;
          font-size: 16px;
          font-weight: bold;
        }
      }
      .description {
        padding-bottom: 10px;
        font-size: 12px;
      }
      .support {
        padding-bottom: 2px;
        overflow: hidden;
        .icon {
          float: left;
          display: inline-block;
          width: 12px;
          height: 12px;
          margin-right: 4px;
          &.decrease {
            .bgImg(decrease_1);
          }
          &.discount {
            .bgImg(discount_1);
          }
          &.special {
            .bgImg(special_1);
          }
          &.invoice {
            .bgImg(invoice_1);
          }
          &.guarantee {
            .bgImg(guarantee_1);
          }
        }
        .text {
          float: left;
          font-size: 10px;
          line-height: 12px;
        }
      }
    }
    .count {
      font-size: 0px;
      background: rgba(0,0,0,0.2);
      border-radius: 14px;
      position: absolute;
      bottom: 18px;
      right: 12px;
      padding: 6px 8px;
      .number {
        font-size: 10px;
      }
      i {
        font-size: 10px;
        margin-left: 4px;
      }
    }

  }
  .noticeWrap {
    position: relative;
    height: 28px;
    line-height: 28px;
    background: rgba(7,17,27,0.2);
    padding: 0 22px 0 12px;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    .notice {
      display: inline-block;
      width: 22px;
      height: 12px;
      .bgImg(bulletin);
    }
    .noticeContent {
      height: 28px;
      margin: 0 4px;
      vertical-align: top;
      font-size: 10px;
      color: #fff;
    }
    i {
      position: absolute;
      font-size: 10px;
      right: 12px;
    }

  }
  .background {
    position: absolute;
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
    z-index: -1;
    filter: blur(10px)
  }
  .detail {
    position: fixed;
    top: 0px;
    left: 0px;
    z-index: 100;
    overflow: auto;
    width: 100%;
    height: 100%;
    background: rgba(7,17,27,0.8);
    .detailWrap {
      padding: 0px 36px;
      min-height: 100%;
      .detailMain {
        margin-top: 64px;
        padding-bottom: 64px;
        .detailTitle {
          text-align: center;
          font-size: 16px;
          font-weight: 700;
          padding: 0 0 28px 0;
        }
        .detailStar {
          text-align: center;
          padding-bottom: 28px;
        }
        .discountMessage {
          text-align: center;
          line-height: 16px;
          span {
            display: inline-block;
            font-size: 14px;
            vertical-align: top;
          }
          .line {
            margin-top: 8px;
            width: 32%;
            border: 1px solid rgba(255, 255, 255, 0.2);
          }
          .discountTitle {
            padding: 0 12px;
          }
        }
        .detailDiscountMessage {
          padding: 12px 12px 26px 12px;
          .message {
            padding-top: 12px;
            height: 16px;
            line-height: 16px;
          }
          span {
            .spanSize(16px,16px)
          }
          .messageIcon {
            &.decrease {
              .bgImg(decrease_2);
            }
            &.discount {
              .bgImg(discount_2);
            }
            &.special {
              .bgImg(special_2);
            }
            &.invoice {
              .bgImg(invoice_2);
            }
            &.guarantee {
              .bgImg(guarantee_2);
            }
          }
          .itemMessage {
            width: auto;
            vertical-align: top;
            padding-left: 6px;
            font-size: 12px;
            line-height: 16px;
          }
        }
        .businessMessage {
          text-align: center;
          line-height: 16px;
          span {
            display: inline-block;
            font-size: 14px;
            vertical-align: top;
          }
          .line {
            margin-top: 8px;
            width: 32%;
            border: 1px solid rgba(255, 255, 255, 0.2);
          }
          .businessTitle {
            padding: 0 12px;
          }
        }
        .businessNotice {
          padding: 24px 12px 0 12px;
          font-size: 12px;
          line-height: 24px;
        }
      }
    }
    .detailClose {
      width: 32px;
      height: 32px;
      margin: -64px auto 0;
      font-size: 32px;
    }
  }
</style>
