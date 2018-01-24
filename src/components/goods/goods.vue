<template>
  <div class="commodity">
    <div class="menuWrap" ref="menuWrap">
      <div>
        <div v-for="(item, index) in goods" @click="selectMenu(index, $event)" class="menuWrapName menuListHook"
             :class="{'current': currentIndex === index}">
          <span class="text"><span class="icon" v-show="item.type > 0" :class="classMap[item.type]"></span>{{item.name}}</span>
        </div>
      </div>
    </div>
    <div class="foodsWrap" ref="foodsWrap">
      <ul>
        <li v-for="item in goods" class="foodList foodListHook">
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
                  <span class="nowPrice">¥{{food.price}}</span><span class="oldPrice" v-show="food.oldPrice">¥{{food.oldPrice}}</span>
                </div>
                <div class="cartControlWrap">
                  <cartControl :food="food"></cartControl>
                </div>
              </div>
            </li>
          </ul>
        </li>
      </ul>
    </div>
    <shopcart :delivery-price="seller.deliveryPrice" :min-price="seller.minPrice"></shopcart>
  </div>
</template>

<script type="text/javascript">
  import BScroll from 'better-scroll';
  import shopcart from '../shopcart/shopcart';
  import cartControl from '../cartControl/cartControl.vue';

  export default {
    props: {
      seller: {
        type: Object
      }
    },
    data () {
      return {
        goods: [],
        classMap: ['decrease', 'discount', 'special', 'invoice', 'guarantee'],
        listHeight: [],
        scrollY: 0
      };
    },
    created: function () {
      this.$http.get('../../../data.json').then((res) => {
        if (res.status === 200) {
          this.goods = res.data.goods;
          this.$nextTick(() => {
            this.scrollFn();
            this.calculationHeight();
          });
        }
      }).catch((err) => {
        console.log(err);
      });
    },
    computed: {
      currentIndex: function () {
        for (let i = 0; i < this.listHeight.length; i++) {
          let height1 = this.listHeight[i];
          let height2 = this.listHeight[i + 1];
          if (!height2 || (this.scrollY >= height1 && this.scrollY < height2)) {
            return i;
          }
        }
        return 0;
      }
    },
    methods: {
      selectMenu: function (index, event) {
        console.log(event);
        // if (!event._constructed) {
        //   return;
        // }
        // 获取右边商品列表，左侧列表索引与右侧列表索引结合
        let foodList = this.$refs.foodsWrap.getElementsByClassName('foodListHook');
        let el = foodList[index];
        this.foodsScroll.scrollToElement(el, 100);
      },
      // 实现滚动的方法
      scrollFn: function () {
        this.menuScroll = new BScroll(this.$refs.menuWrap, {click: true});
        this.foodsScroll = new BScroll(this.$refs.foodsWrap, {probeType: 3});
        this.foodsScroll.on('scroll', (pos) => {
          this.scrollY = Math.abs(Math.round(pos.y));
        });
      },
      calculationHeight: function () {
        // 计算右侧每栏的高度
        let foodList = this.$refs.foodsWrap.getElementsByClassName('foodListHook');
        let height = 0;
        this.listHeight.push(height);
        for (let i = 0; i < foodList.length; i++) {
          let item = foodList[i];
          height += item.clientHeight;
          this.listHeight.push(height);
        };
      }
    },
    components: {
      shopcart,
      cartControl
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
    bottom: 48px;
    width: 100%;
    overflow: hidden;
    .menuWrap {
      flex: 0 0 80px;
      width: 80px;
      background: #f3f5f7;
      .menuWrapName {
        height: 54px;
        font-size: 12px;
        color: rgb(77, 85, 93);
        padding: 0 12px;
        display: table;
        &.current {
          position: relative;
          margin-top: -1px;
          background: #fff;
          z-index: 10;
          font-width: 700;
          .text {
            border: none;
          }
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
        &:last-child .text {
          border: none;
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
              flex: 1;
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
                font-weight: 700;
                .nowPrice {
                  color: rgb(240, 20, 20);
                  font-size: 14px;
                  padding-right: 8px;
                }
                .oldPrice {
                  text-decoration: line-through;
                  font-size: 10px;
                  color: rgb(147, 153, 159);
                }
              }
              .cartControlWrap {
                position: absolute;
                right: 10px;
              }
            }
          }
        }
      }
    }
  }
</style>
