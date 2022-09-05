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
const { x, y } = useMouse()
const { x: x2, y: y2 } = useMouse({ eventFilter: debounceFilter(100) })
</script>

<template>
  <div class="g-container">
    <p>Lorem ipsum dolor sit amet</p>
    <div id="g-pointer-1" :style="{ transform: `translate(${x}px, ${y}px)` }"></div>
    <div id="g-pointer-2" :style="{ transform: `translate(${x2 - 15}px, ${y2 - 15}px)` }"></div>
  </div>
</template>

<style scoped>
.g-container {
  position: relative;
  width: 100%;
  height: 100%;
  cursor: none;
  background-color: #eee;
  overflow: hidden;
  display: flex;
}

.g-container p {
  position: relative;
  margin: auto;
  color: #000;
  font-size: 64px;
}

#g-pointer-1,
#g-pointer-2 {
  position: absolute;
  top: 0;
  left: 0;
  width: 12px;
  height: 12px;
  background: #999;
  border-radius: 50%;
  background-color: #fff;
  mix-blend-mode: exclusion;
  z-index: 1;
}

#g-pointer-2 {
  width: 42px;
  height: 42px;
  background: #222;
  transition: 0.2s ease-out;
}
</style>