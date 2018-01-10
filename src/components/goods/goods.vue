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
          <h1 class="title">{{item.name}}</h1>
          <ul>
            <li v-for="food in item.foods" class="itemFood"></li>
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
    }
  }
</style>
