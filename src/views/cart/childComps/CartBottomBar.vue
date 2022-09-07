<template>
  <div class="bottom-bar">
    <div class="check-content">
      <check-button 
                  @click.native="checkClick"
                  :is-checked="isSelectAll" 
                  class="check-button" />
      <span>全选</span>
    </div>
    <div class="price">
      合计：¥{{totalPrice}}
    </div>
    <div class="calculate" @click="calcClick">
      去计算({{checkLength}})
    </div>
  </div>
</template>

<script>
  import CheckButton from 'components/content/checkButton/CheckButton';

  import {mapGetters} from 'vuex';

  export default {
    name: 'CartBottomBar',
    components: {
      CheckButton,
    },
    computed: {
      ...mapGetters(['cartList']),
      totalPrice() {
        return this.cartList
        .filter(item => item.checked)
        .reduce((preValue, item) => preValue + item.price * item.count, 0)
      },
      checkLength() {
        return this.cartList.filter(item => item.checked).length
      },
      isSelectAll() {
        // return !(this.cartList.filter(item => !item.checked).length)
        if (this.cartList.length === 0) return false
        return !(this.cartList.find(item => !item.checked))
      }
    },
    methods: {
      checkClick() {
        if (this.isSelectAll) { //全部选中
          this.cartList.forEach(item => item.checked = false)
        } else {
          this.cartList.forEach(item => item.checked = true)
        }
      },
      calcClick() {
        if (!this.checkLength) {
          this.$toast.show('请选择购买的商品', 1000)
        }
      }
    }
  }
</script>

<style scoped>
  .bottom-bar {
    display: flex;
    height: 35px;
    line-height: 35px;
    background-color: #eee;
  }

  .check-content {
    display: flex;
    align-items: center;
    margin-left: 5px;
    width: 80px;
  }

  .check-button {
    width: 22px;
    height: 22px;
    line-height: 22px;
    margin-right: 5px;
  }

  .price {
    color: rgb(82, 82, 82);
    flex: 1;
  }

  .calculate {
    width: 90px;
    text-align: center;
    background-color: rgb(255, 90, 29);
    color: #fff;
  }
</style>