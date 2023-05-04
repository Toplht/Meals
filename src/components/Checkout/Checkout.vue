<script setup>
import { useMealsStore } from '../../store/meals'
import Counter from '../UI/Counter.vue'

const props = defineProps(['isShow'])
const emits = defineEmits(['close'])
const meals = useMealsStore()
</script>

<template>
  <div class="checkout" v-show="props.isShow">
    <div class="close">
      <i class="ri-close-fill" @click="$emit('close')"></i>
    </div>
    <!-- 订单详情页 -->
    <div class="detail">
      <div class="header">餐品详情</div>
      <div class="food">
        <div class="item" v-for="item in meals.cartMeals">
          <div class="img-wrap">
            <img :src="item.img" :alt="item.title">
          </div>
          <div class="info">
            <h2 class="title">{{ item.title }}</h2>
            <div class="count">
              <Counter :meal="item"></Counter>
              <span class="amount">{{ item.count * item.price }}</span>
            </div>
          </div>
        </div>
      </div>
      <div class="total">合计￥<span class="money">{{ meals.amount }}</span></div>
    </div>
    <div class="bar">
      <div class="total-amount">
        <p class="no-goods" v-show="meals.totalCount <= 0">未选购商品</p>
        <P class="has-goods" v-show="meals.totalCount > 0" @click="showDetails = true">{{ meals.amount }}</P>
      </div>

      <button class="checkout-btn">支付</button>
    </div>
  </div>
</template>

<style scoped>
.checkout {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: rgb(240, 240, 240);
  z-index: 99999;
}

.close {
  height: 60rem;
  line-height: 60rem;
  padding-left: 20rem;
  font-size: 36rem;
  font-weight: bold;
}

.detail {
  background-color: white;
  margin: 0 20rem;
  border-radius: 30rem;
}

.header {
  height: 120rem;
  line-height: 120rem;
  font-size: 36rem;
  font-weight: bold;
  padding: 0 40rem;
  border-bottom: 1px dashed #e6e6e6;
}

.food {
  background-color: white;
  max-height: 800rem;
  overflow: auto
}

.total {
  position: relative;
  background-color: white;
  height: 140rem;
  line-height: 140rem;
  font-size: 28rem;

  text-align: right;
  padding-right: 40rem;
  border-top: 1px dashed #e6e6e6;
  border-radius: 30rem;
}

.total::before,
.total::after {
  content: '';
  background-color: rgb(240, 240, 240);
  position: absolute;
  border-radius: 50%;
  width: 30rem;
  height: 30rem;
  left: -15rem;
  top: -15rem;
}

.total::after {
  left: auto;
  right: -15rem;
}

.money {
  font-size: 40rem;
  font-weight: bold;
}

.item {
  display: flex;
}

.img-wrap {
  width: 160rem;
}

.info {
  flex: auto;
}

.title {
  margin-top: 30rem;
  font-size: 30rem;
  font-weight: bold;
}

.count {
  display: flex;
  justify-content: space-between;
  margin-top: 40rem;
  margin-right: 30rem;
}

.amount {
  font-size: 30rem;
  font-weight: bold;
}

.amount::before {
  content: '￥';
  font-weight: normal;
  font-size: 24rem;
}

.bar {
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


.total-amount {
  margin-left: 60rem;
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
  content: '合计 : ￥';
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