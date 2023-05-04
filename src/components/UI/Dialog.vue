<script setup>
import Mask from './Mask.vue';
/* 定义操作信息 */
const props = defineProps(['msg'])
const emits = defineEmits(['confirm'])
</script>

<!-- 定义一个对话框组件 -->
<!-- Dialog组件由两部分组成：对话框和mask -->
<template>
  <Mask>
    <div class="dialog">
      <p class="msg">{{ props.msg }}</p>
      <div class="btn">
        <!-- 利用了透传，Mask内的模板代码通过插槽的方式最终是在Mask组件中被渲染，就相当于在
             Mask中写的，所以可以直接使用Mask组件中定义的属性和方法 -->
        <button @click="$emit('hide')" class="cancel">取消</button>
        <button @click="$emit('confirm')" class="confirm">确认</button>
      </div>
    </div>
  </Mask>
</template>

<style scoped>
.dialog {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 700rem;
  height: 300rem;
  background-color: white;
  margin: 200rem auto 0;
  border-radius: 40px;
}

.msg {
  height: 200rem;
  font-size: 36rem;
  font-weight: bold;
  /* 设置行高 */
  line-height: 200rem;
  color: black;
}

.btn {
  position: absolute;
  width: 80%;
  bottom: 20rem;
  display: flex;
  justify-content: space-around;
}

button {
  width: 140rem;
  height: 50rem;
  font-size: 30rem;
  border-radius: 20px;
  text-align: center;
  border: 1px solid gray;
  background-color: white;
}

.confirm {
  background-color: rgb(248, 188, 0);
}
</style>