<script setup lang="ts">
import { ref, unref, onMounted, onUnmounted } from 'vue'

function useEventListener(target, event, callback) {
  // 也可以用字符串形式的 CSS 选择器来寻找目标 DOM 元素
  onMounted(() => target.addEventListener(event, callback))
  onUnmounted(() => target.removeEventListener(event, callback))
}

function useMouse() {
  const x = ref(0)
  const y = ref(0)
  useEventListener(window, 'mousemove', (event) => {
    x.value = event.pageX
    y.value = event.pageY
  })

  return { x, y }
}

const { x, y } = useMouse()
// const mouse = reactive(useMouse())
</script>

<template>鼠标的位置在 {{ x }}, {{ y }}</template>