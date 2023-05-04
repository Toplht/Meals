<script setup>
import { ref } from 'vue';
import { useMealsStore } from '../../store/meals';
import Meals from '../Meals/Meals.vue';
import Dialog from '../UI/Dialog.vue';
import Mask from '../UI/Mask.vue';
const meals = useMealsStore()
const showDialog = ref(false)
const emits = defineEmits()

const okHandler = () => {
  /* 
    1. 关闭对话框
    2. 清空购物车
    3. 关闭餐品详情页
  */

  showDialog.value = false
  meals.clearCart()
  emits('hide')

}
</script>

<template>
  <!-- Mask组件为该组件中根元素 -->
  <Mask style="z-index: 999;">
    <Dialog @confirm="okHandler" msg="确认清空购物车吗？" @hide="showDialog = false" :isShow="showDialog"></Dialog>
    <div class="cart-details">
      <div class="header">
        <h2>餐品详情</h2>
        <a @click="showDialog = true" href="javescript:;">
          <i class="ri-delete-bin-line"></i>
          清空购物车
        </a>
      </div>
      <Meals :desc="false" :meals="meals.cartMeals"></Meals>
    </div>
  </Mask>
</template>

<style scoped>
.cart-details {
  position: absolute;
  width: 100%;
  bottom: 0;
  background-color: white;
  border-top-left-radius: 40rem;
  border-top-right-radius: 40rem;
  /* 设置滚动条 */
  overflow: auto;
}

/* 给组件Meals中的外层容器<div class="meals"></div>
 设置样式，该样式只有当子组件在父组件中渲染时生效，会把原先的覆盖 */
.meals {
  height: auto;
  max-height: calc(280rem*4);
}

.header {
  position: fixed;
  width: 100%;
  display: flex;
  justify-content: space-between;
  padding: 20rem 40rem;
  background-color: white;
  border-top-left-radius: 40rem;
  border-top-right-radius: 40rem;
}

.header h2 {
  font-size: 28rem;
}

.header a {
  display: flex;
  align-items: center;
  color: gray;
  font-size: 24rem;
}

.header i {
  margin-right: 8rem;
}
</style>

