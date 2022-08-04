<script setup lang="ts">
import { ref, watchEffect } from 'vue'

const count = ref(0)
watchEffect(() => console.log(count.value))

function addCount() {
  count.value++
}
</script>

<template>
  <p>你点击了 {{ count }} 次
    <span @click="addCount()" class="border px-2">
      点击
    </span>
  </p>
</template>
