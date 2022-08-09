
<template>
  <div class="g-container">
    <div class="word" style="--word-delay: -16s">返回由 Ref 组成的对象</div>
    <div class="word" style="--word-delay: -14s">副作用自动清除</div>
    <div class="word" style="--word-delay: -12s">接受 Ref 作为函数参数</div>
    <div class="word" style="--word-delay: -10s">使用 ref / unref / MaybeRef</div>
    <div class="word" style="--word-delay: -8s">抽离组合式函数</div>
    <div class="word" style="--word-delay: -6s">建立 “连结”</div>
    <div class="word" style="--word-delay: -4s">使用 shallowRef</div>
    <div class="word" style="--word-delay: -2s">异步操作转为 同步</div>
  </div>
</template>

<style scoped>
.g-container {
  position: relative;
  width: 100%;
  height: 100%;
  background: #121212;
  font-family: 'Montserrat', sans-serif;
  color: #fff;
  font-size: 70px;
  filter: contrast(15);
}

.word {
  position: absolute;
  width: 100%;
  text-align: center;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  animation: change 16s infinite ease-in-out;
  animation-delay: var(--word-delay);
}

@keyframes change {

  0%,
  5%,
  100% {
    filter: blur(0px);
    opacity: 1;
  }

  40%,
  86% {
    filter: blur(80px);
    opacity: 0;
  }
}
</style>