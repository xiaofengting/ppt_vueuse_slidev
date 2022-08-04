<script setup lang="ts">
import { ref, unref, onMounted, onUnmounted } from 'vue'

function useEventListener(target, event, callback) {
  // 也可以用字符串形式的 CSS 选择器来寻找目标 DOM 元素
  onMounted(() => target.addEventListener(event, callback))
  onUnmounted(() => target.removeEventListener(event, callback))
}

function debounceFilter(ms: number) {
  let timer
  const filter = (invoke) => {
    const duration = unref(ms)
    if (timer)
      clearTimeout(timer)
    if (duration <= 0) {
      return invoke()
    }
    timer = setTimeout(() => {
      invoke()
    }, duration)
  }
  return filter
}

type eventFilterFn = (invoke) => {}
type useMouseOption = { eventFilter?: eventFilterFn }
function useMouse(options: useMouseOption = {}) {
  const { eventFilter } = options
  const x = ref(0)
  const y = ref(0)

  const mouseHandler = (event: MouseEvent) => {
    x.value = event.pageX
    y.value = event.pageY
  }

  const mouseHandlerWrapper = (event: MouseEvent) => {
    return eventFilter === undefined ? mouseHandler(event) : eventFilter(() => mouseHandler(event))
  }

  useEventListener(window, 'mousemove', mouseHandlerWrapper)

  return { x, y }
}
const { x, y } = useMouse({ eventFilter: debounceFilter(200) })
</script>

<template>鼠标的位置在 {{ x }}, {{ y }}</template>