<script setup>
import { useMealsStore } from '../../store/meals';

const meals = useMealsStore()
const props = defineProps(['meal'])
</script>

<template>
  <div class="counter">
    <template v-if="props.meal.count > 0">
      <button class="sub" @click="meals.subMealFromCart(props.meal)"><i class="ri-subtract-line"></i></button>
      <span>{{ props.meal.count }}</span>
    </template>
    <button class="add" @click="meals.addMealToCart(props.meal)"><i class="ri-add-fill"></i></button>
  </div>
</template>

<style scoped>
.counter {
  display: flex;
  align-items: center;
}

.sub,
.add {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 30rem;
  height: 30rem;
  background-color: rgb(234, 178, 0);
  border: none;
  border-radius: 50%;
  font-size: 30rem;
  font-weight: bold;
}

.sub {
  background-color: #fff;
  border: 1px solid black;
}

span {
  font-size: 30rem;
  margin: 0 10rem;
}
</style>