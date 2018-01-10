<template>
  <div id="app">
    <v-herader :seller="seller"></v-herader>
    <div class="tab">
      <div class="tabItem">
        <router-link to="/goods">商品</router-link>
      </div>
      <div class="tabItem">
        <router-link to="/comment">评论</router-link>
      </div>
      <div class="tabItem">
        <router-link to="/seller">商家</router-link>
      </div>
    </div>
    <div class="content">
      <router-view :seller="seller"></router-view>
    </div>
  </div>
</template>

<script type="text/javascript">
  import header from './components/header/header.vue';
  export default {
    data () {
      return {
        seller: {}
      };
    },
    created: function () {
      this.$http.get('/data.json').then((res) => {
        if (res.status === 200) {
          this.seller = res.data.seller;
        }
      }).catch((err) => {
        console.log(err);
      });
    },
    methods: {
    },
    components: {
      'v-herader': header
    }
  };
</script>

<style lang="less">
  .tab {
    width: 100%;
    display: flex;
    border-bottom: 1px solid rgba(7, 17, 27, 0.1);
    .tabItem {
      flex: 1;
      text-align: center;
      height: 40px;
      line-height: 40px;
      & > a {
        font-size: 14px;
        color: rgb(77, 85, 93);
        display: block;
        &.active {
          color: rgb(240, 20, 20);
        }
      }
    }
  }
</style>
