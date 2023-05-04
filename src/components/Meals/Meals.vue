<script setup>
import Meal from './Meal.vue';

const props = defineProps(['meals'])
</script>
<template>
  <!-- 所有汉堡的容器 -->
  <!-- 透传后根元素被渲染 -->
  <!-- <div class="meals" :meals="meals.cartMeals" :desc="true或者false"></div> -->
  <div class="meals">
    <!-- 显示商品信息 -->
    <!-- 使用$attrs访问透传对象 -->
    <Meal :desc="$attrs.desc" :meal="item" v-for="item in props.meals"></Meal>
    <!-- props.meals.length == 0 要放后面防止逻辑中断 -->
    <template v-if="!props.meals || props.meals.length == 0">
      <h2>没有找到商品</h2>
    </template>
  </div>
</template>

<style scoped>
.meals {
  /* 防止高度太大导致整个body出现滚动条 */
  height: calc(100vh - 120rem);
  /* 自动出现滚动条 */
  overflow: auto;
  padding-bottom: 140rem;
}
</style>