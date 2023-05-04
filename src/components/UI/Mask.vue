<script setup>
import { ref } from 'vue'

const props = defineProps(['isShow'])
const emit = defineEmits(['hide'])
</script>

<template>
  <Teleport to="body">
    <!-- 使用:="$attrs指定透传 -->
    <!-- @click.self="$emit('hide')" 的作用时防止事件冒泡 -->
    <div :="$attrs" class="mask" v-show="props.isShow" @click.self="$emit('hide')">
      <!-- 使用插槽接收模板内容，让子组件在它们的组件中渲染这些片段 -->
      <slot></slot>
    </div>
  </Teleport>
</template>

<style scoped>
.mask {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: rgba(0, 0, 0, 0.3);
  z-index: 99999;
}
</style>