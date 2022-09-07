<template>
  <div class="cart">
    <nav-bar class="nav-bar">
      <div slot="center">购物车({{length}})</div>
    </nav-bar>
    <!-- 商品列表 -->
    <scroll class="cart-content" ref="scroll">
      <cart-list></cart-list>
    </scroll>
    <!-- 底部汇总 -->
    <cart-bottom-bar class="cart-bottom-bar" />
  </div>
</template>

<script>
  
  import CartList from './childComps/CartList'
  import CartBottomBar from './childComps/CartBottomBar'

  import NavBar from 'components/common/navbar/NavBar'
  import Scroll from 'components/common/scroll/Scroll'

  import {mapGetters} from 'vuex';

  export default {
    name: "Cart",
    components: {
      CartList,
      CartBottomBar,
      NavBar,
      Scroll,
    },
    computed: {
      ...mapGetters({
        length: 'cartLength',
      })
    },
    activated() {
      this.$refs.scroll.refresh()
    }
  }
</script>

<style scoped>
  .cart {
    height: 100vh;
    position: relative;
  }
  
  .nav-bar {
    background-color: var(--color-tint);
    color: #fff;
  }

  .cart .cart-content {
    overflow: hidden;
    position: absolute;
    top: 44px;
    bottom: 84px;
    left: 0;
    right: 0;
  }

  .cart-bottom-bar {
    position: absolute;
    bottom: 49px;
    left: 0;
    right: 0;
  }
</style>