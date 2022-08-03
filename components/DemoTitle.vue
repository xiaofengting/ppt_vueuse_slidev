<script setup lang="ts">
import { useTitle } from '@vueuse/core'
const title = useTitle(null)
</script>

<template>
  <span class="mr-5">修改title：</span>
  <input class="mt-10 border" v-model="title" type="text">
</template>