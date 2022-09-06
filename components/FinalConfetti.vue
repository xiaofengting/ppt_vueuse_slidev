<script setup>
import confetti from 'canvas-confetti'
import { whenever } from '@vueuse/core'
import { useMagicKeys } from '@vueuse/core'

function fire() {
  const end = Date.now() + (1 * 1000);
  const colors = ['#bb0000', '#ffffff'];
  (function frame() {
    confetti({
      particleCount: 2, angle: 60, spread: 55,
      origin: { x: 0 }, colors: colors
    });
    confetti({
      particleCount: 2, angle: 120, spread: 55,
      origin: { x: 1 }, colors: colors
    });
    if (Date.now() < end) {
      requestAnimationFrame(frame);
    }
  }());
}

const { q_w } = useMagicKeys()
whenever(q_w, () => { fire() })

whenever(
  () => $slidev.nav.currentPage === 42,
  () => {
    fire()
  }
)
</script>
<template>
  <div />
</template>
