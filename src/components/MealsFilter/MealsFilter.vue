<script setup>
import { useMealsStore } from '../../store/meals';

const meals = useMealsStore()
</script>
<template>
  <div class="filter">
    <div class="filter-inner">
      <i class="ri-search-line"></i>
      <input v-model="meals.keyword" type="text" placeholder="请输入关键字">
    </div>
  </div>
</template>

<style scoped>
.filter {
  padding: 20rem 40rem;
  border-bottom: 1px solid #e6e6e6;
}

.filter-inner {
  display: flex;
  align-items: center;
  height: 80rem;
  /* 使父元素内的子元素相对于于父元素进行定位 */
  position: relative;
}

input {
  background-color: rgb(242, 242, 242);
  border: none;
  outline: none;
  width: 100%;
  height: 100%;
  border-radius: 40rem;
  padding-left: 80rem;
}

.filter-inner i {
  /* 使用实现绝对定位脱离文档流 */
  position: absolute;
  color: rgb(184, 184, 184);
  font-size: 30rem;
  margin-left: 30rem;

}
</style>