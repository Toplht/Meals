<script setup>
import Counter from '../UI/Counter.vue'
const props = defineProps(['meal', 'desc'])
</script>
<template>
  <div class="meal">
    <!-- 汉堡图片 -->
    <div class="img">
      <img :src="props.meal.img" alt="">
    </div>
    <!-- 汉堡信息 -->
    <div class="info">
      <div class="desc">
        <h2>{{ props.meal.title }}</h2>
        <!-- desc为自定义属性，类型为布尔值，true则描述，false不描述 -->
        <p v-show="desc">{{ props.meal.desc }}</p>
      </div>
      <div class="price-btn">
        <span class="price">{{ props.meal.price }}</span>
        <Counter :meal="props.meal"></Counter>
      </div>
    </div>
  </div>
</template>

<style scoped>
.meal {
  /* 弹性盒子默认水平排列 */
  display: flex;
  height: 280rem;
  align-items: center;
  border-bottom: 1px #e6e6e6 solid;
  padding: 0 20rem;
}

.img {
  width: 200rem;
  vertical-align: middle;
}

.info {
  width: 450rem;
  margin-left: 10rem;
}

.info h2 {
  color: black;
  font-size: 30rem;
  font-weight: normal;
}

.info p {
  font-size: 24rem;
  color: #9f9f9f;
}

.price-btn {
  margin-top: 40rem;
  display: flex;
  justify-content: space-between;
}

.price {
  font-size: 30rem;
  font-weight: bold;
}

/* 利用伪元素加上美元符号 */
.price::before {
  content: "￥";
}
</style>