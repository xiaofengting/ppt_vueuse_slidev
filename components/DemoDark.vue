<script setup lang="ts">
import { computed } from 'vue'
import { usePreferredDark, useColorMode, useToggle } from '@vueuse/core'

function useDark() {
  const preferredDark = usePreferredDark()
  const mode = useColorMode()

  return computed<boolean>({
    get() {
      return mode.value === 'dark'
    },
    set(v) {
      if (v === preferredDark.value)
        mode.value = 'auto'
      else
        mode.value = v ? 'dark' : 'light'
    }
  })
}

const isDark = useDark()
const toggleDark = useToggle(isDark)
</script>

<template>
  <button
    class="bg-green-400 rounded border-b-2 border-green-900 text-white text-sm px-2 pt-1.5 pb-1 inline-block !outline-none hover:bg-opacity-85 mt-10"
    @click="toggleDark()">
    <carbon:moon v-if="isDark" />
    <carbon:sun v-else />

    <span class="mr-1 ml-2">{{ isDark ? 'Dark' : 'Light' }}</span>
  </button>
</template>