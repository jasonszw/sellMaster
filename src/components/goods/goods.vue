<template>
  <div class="commodity">
    <div class="menuWrap">
      <div v-for="(item, index) in goods" @click="selectMenu(index, $event)" class="menuWrapName" :class="{'current': currentIndex === index}">
        <span class="text"><span class="icon" v-show="item.type > 0" :class="classMap[item.type]"></span>{{item.name}}</span>
      </div>
    </div>
    <div class="foodsWrap">
      <ul>
        <li v-for="item in goods" class="foodList">
          <p class="title">{{item.name}}</p>
          <ul>
            <li v-for="food in item.foods" class="itemFood">
              <div class="icon">
                <img :src="food.icon">
              </div>
              <div class="content">
                <p class="name">{{food.name}}</p>
                <p class="description" v-show="food.description">{{food.description}}</p>
                <div class="praiseRate">
                  <span>月售{{food.sellCount}}份</span><span>好评率{{food.rating}}%</span>
                </div>
                <div class="price">
                  <span>¥{{food.price}}</span><span v-show="food.oldPrice">¥{{food.oldPrice}}</span>
                </div>
              </div>
            </li>
          </ul>
        </li>
      </ul>
    </div>
  </div>
</template>

<script type="text/javascript">
  export default {
    props: {
      seller: {
        type: Object
      }
    },
    data () {
      return {
        goods: [],
        classMap: ['decrease', 'discount', 'special', 'invoice', 'guarantee']
      };
    },
    created: function () {
      this.$http.get('../../../data.json').then((res) => {
        if (res.status === 200) {
          this.goods = res.data.goods;
        }
      }).catch((err) => {
        console.log(err);
      });
    },
    computed: {
      currentIndex: function () {
      }
    },
    methods: {
      selectMenu: function (index, event) {
        console.log(index, event);
      }
    }
  };
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="less">
  @import "../../assets/less/mixin";
  .commodity {
    display: flex;
    position: absolute;
    top: 177px;
    bottom: 36px;
    width: 100%;
    overflow: hidden;
    .menuWrap {
      flex: 0 0 80px;
      width: 80px;
      background: #f3f5f7;
      .menuWrapName {
        height: 54px;
        font-size: 12px;
        color: rgb(77,85,93);
        padding: 0 12px;
        display: table;
        &.current {
          position: relative;
          margin-top: -1px;
          background: #fff;
          z-index: 10;
          font-width: 700;
          border: none;
        }
        .text {
          display: table-cell;
          vertical-align: middle;
          width: 56px;
          line-height: 14px;
          border-bottom: 1px solid rgba(7, 17, 27, 0.2);
          .icon {
            width: 12px;
            height: 12px;
            display: inline-block;
            vertical-align: top;
            margin-right: 2px;
            &.decrease {
              .bgImg(decrease_3);
            }
            &.discount {
              .bgImg(discount_3);
            }
            &.special {
              .bgImg(special_3);
            }
            &.invoice {
              .bgImg(invoice_3);
            }
            &.guarantee {
              .bgImg(guarantee_3)
            }
          }
        }
      }
    }
    .foodsWrap {
      flex: 1;
      .foodList {
        .title {
          height: 26px;
          line-height: 26px;
          font-size: 12px;
          color: rgb(147, 153, 159);
          padding-left: 14px;
          background: #f3f5f7;
          border-left: 4px solid #d9dde1;
        }
        ul {
          .itemFood {
            display: flex;
            margin: 0px 18px;
            padding: 18px 0px;
            border-bottom: 1px solid rgba(7, 17, 27, 0.1);
            &:last-child {
              border: none;
            }
            .icon {
              flex: 0 0 57px;
              img {
                width: 57px;
                height: 57px;
              }
            }
            .content {
              flex: auto;
              padding-left: 10px;
              .name {
                font-size: 14px;
                padding-top: 2px;
                color: rgb(7, 17, 27);
              }
              .description, .praiseRate {
                font-size: 10px;
                color: rgb(147, 153, 159);
                line-height: 10px;
              }
              .description {
                padding-top: 8px;
              }
              .praiseRate {
                padding: 8px 0;
                span:nth-of-type(1) {
                  padding-right: 12px;
                }
              }
              .price {
                span:nth-of-type(1) {
                  color: rgb(240, 20, 20);
                  font-size: 14px;
                  font-weight: 700;
                  padding-right: 8px;
                }
              }
            }
          }
        }
      }
    }
  }
</style>
