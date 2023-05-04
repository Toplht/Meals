<script setup>
import cartBag from '../../assets/bag.png'
import { useMealsStore } from '../../store/meals';
import { ref } from 'vue'
import CartDetails from './CartDetails.vue';
import Checkout from '../Checkout/Checkout.vue';

const meals = useMealsStore()
const showDetails = ref(false)
const showCheckout = ref(false)
const close = () => {
  showCheckout.value = false
}
</script>
<template>
  <Checkout :is-show="showCheckout" @close="close"></Checkout>
  <!-- 利用透传将父组件的属性传给根元素 -->
  <!-- 相当于 <Mask :is-show="showDetails" @hide="showDetails = false"></Mask>，即把值传递给了Mask组件的自定义属性和自定义事件 -->
  <!-- Mask组件 再透传给组件中的根元素 div 相当于
   <div :="$attrs" 
        class="mask" 
        v-show="props.isShow"
        @click.self="$emit('hide')"> -->
  <CartDetails :is-show="showDetails" @hide="showDetails = false"></CartDetails>
  <div class="cart-bar">
    <div class="cart-bag">
      <img :src="cartBag" alt="">
      <span v-show="meals.totalCount > 0" class="total-count">{{ meals.totalCount }}</span>
    </div>

    <div class="total-amount">
      <p class="no-goods" v-show="meals.totalCount <= 0">未选购商品</p>
      <P class="has-goods" v-show="meals.totalCount > 0" @click="showDetails = true">{{ meals.amount }}</P>
    </div>

    <button class="checkout-btn" @click="showCheckout = meals.totalCount > 0">去结算</button>
  </div>
</template>

<style scoped>
.cart-bar {
  /* 使用固定定位 */
  position: fixed;
  width: 710rem;
  height: 100rem;
  left: 0;
  right: 0;
  margin: 0 auto;
  background-color: rgb(58, 58, 58);
  bottom: 40rem;
  border-radius: 60rem;
  z-index: 9999;
}

.cart-bag {
  width: 100rem;
  position: absolute;
  bottom: -10rem;
}

.total-count {
  width: 40rem;
  height: 40rem;
  text-align: center;
  line-height: 40rem;
  position: absolute;
  background-color: red;
  border-radius: 50%;
  color: white;
  font-size: 20rem;
  font-weight: bold;
  left: 80rem;
}

.total-amount {
  margin-left: 140rem;
  line-height: 100rem;
}

.no-goods,
.has-goods {
  color: rgb(148, 148, 148);
  font-size: 36rem;
  font-weight: bold;
}

.has-goods {
  color: white;
}

.has-goods::before {
  content: '￥';
  font-size: 24rem;
  font-weight: bold;
}

.checkout-btn {
  position: absolute;
  top: 0;
  right: 0;
  width: 200rem;
  height: 100%;
  border-radius: 60rem;
  border: none;
  background-color: rgb(248, 188, 0);
  font-size: 36rem;
  font-weight: bold;
}
</style>