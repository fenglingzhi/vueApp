<template>
  <div>
    <v_header v-bind:seller='seller'></v_header>
    <div class="tab border-1px">
      <div class="tab-item">
        <a v-link="{path: '/goods'}">商品</a>
      </div>
      <div class="tab-item">
        <a v-link="{path: '/ratings'}">评论</a>
      </div>
      <div class="tab-item">
        <a v-link="{path: '/seller'}">商家</a>
      </div>
    </div>
    <router-view></router-view>

  </div>
</template>
<style lang="stylus" rel="stylesheet/stylus">
  @import "./common/stylus/mixin.styl"
  .tab
    display:flex
    width:100%
    line-height : 40px
    height:40px
    /*border-bottom 1px solid rgba(7,17,21,.1)*/
    border-1px(rgba(7,17,21,.1))
    .tab-item
      flex :1
      text-align: center
      & > a
        display : block
        font-size 14px
        color rgb(77,85,93)
        &.active
          color: #f01414
</style>

<script type="text">
  import header from './components/header/header.vue';
  const ERR_OK = 0;
  export default {
      data() {
        return {
          seller: {

          }
        };
      },
      created() {
        this.$http.get('/api/seller').then((response) => {
          response = response.body;
          console.log(response)
          if(response.errno === ERR_OK){
            this.seller = response.data;
            console.log(this.seller);
          }
        });
      },
      components: {
        v_header: header
      }
  };
</script>


