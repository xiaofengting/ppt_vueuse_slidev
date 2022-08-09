---
theme: default
title: Vue 3
highlighter: shiki
---

# 可组合的 Vue

编写可组合可复用的 Vue 函数

<div class="abs-br !mx-14 my-12">
  <div class="mb-3">
  贺晋飞
  </div>
</div>


---
layout: center
class: text-center
---

# Composable

组合式


---

# React Hooks

React 16.8 提供的新特性，为函数组件提供状态、生命周期等。  
使得组件自身能够通过某种机制再触发状态的变更并且引起 re-render。

```ts {all|5|9,10}
import React, { useState } from 'react';

function Example() {
  // 声明一个叫 "count" 的 state 变量
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}
```


---

# React Hooks

&nbsp;

- 过去几年中，发生的最大的一个开发范式层面的一个变化

- 已经彻底取代了 Class 组件。

- 启发了很多组件逻辑表达和逻辑复用的新范式：

<div class="flex justify-evenly mt-10">

Vue

Svelte

SolidJS

</div>


---

# 什么是组合式 API ？

Vue 3 中引入的一种新的编写 Vue 的方式。

<div class="grid grid-cols-2 gap-x-4">

<div>

```html {all|3-4|5-6|7-10|14-15}
<script setup lang="ts">
import { ref, watchEffect } from 'vue'
// 状态
const count = ref(0)
// 副作用
watchEffect(() => console.log(count.value))
function addCount() {
  // 状态更新
  count.value++
}
</script>

<template>
  <p>你点击了 {{ count }} 次</p>
  <button @click="addCount()">点击</button>
</template>
```

<DemoFirst />

</div>

- 基于依赖追踪的范式

- 一次调用，符合原生 JS 直觉

- 自动追踪依赖，无需手动声明


</div>



---
clicks: 4
---

# 对象式 API 与 组合式 API

<div class="grid grid-cols-2 gap-x-4">

```html {all|3,7,8,12,13,17|4-6|8-12|13-17} {at:0}
<script>
export default {
  data() {
    return {
      dark: false
    }
  },
  computed: {
    light() {
      return !this.dark
    }
  },
  methods: {
    toggleDark() {
      this.dark = !this.dark
    }
  }
}
</script>
```

```html {all|1|4|5|7-9} {at:0}
<script setup>
import { ref, computed } from 'vue'

const dark = ref(false)
const light = computed(() => !dark.value)

function toggleDark() {
  dark.value = !dark.value
}
</script>
```

</div>


---

# 什么是组合式函数 ？

利用 Vue 组合式 API 来封装和复用有状态逻辑的函数。

<v-click>

**无状态逻辑**：接收一些输入后立刻返回所期望的输出。

```ts
let list = [0, 1, 2, 3, 4]
let result = list.map(i => i * 2)
list.pop()
result = list.map(i => i * 2)
```

</v-click>

<v-click>

**有状态逻辑**：管理会随时间而变化的状态。

```ts
import { useArrayMap } from '@vueuse/core'
const list = ref([0, 1, 2, 3, 4])
const result = useArrayMap(list, i => i * 2)
// result.value: [0, 2, 4, 6, 8]
list.value.pop()
// result.value: [0, 2, 4, 6]
```

</v-click>


---
clicks: 2
---

# Mixin 与 组合式函数

复用

<div class="grid grid-rows-2 grid-cols-2 gap-x-4">

```js {all|4,8,9,10|0} {at:0}
export default {
  data() {
    return {
      dark: false
    }
  },
  methods: {
    toggleDark() {
      this.dark = !this.dark
    }
  }
}
```

```js {all|3-7|0} {at:0}
import { ref } from 'vue'
export function useMouse() {
  const dark = ref(false)
  function toggleDark() {
    dark.value = !dark.value
  }
  return { dark, toggleDark }
}
```

```html {all|0|4} {at:0}
<script>
import myMixin from './myMixin.js'
export default {
  mixins: [myMixin]
}
</script>
```

```html {all|0|2-4} {at:0}
<script setup>
import { useMouse } from './dark.js'

const { dark, toggleDark } = useMouse()
</script>
```

</div>

---
clicks: 3
---

# Mixin 与 组合式函数

&nbsp;

<v-click>

- 不清晰的 property 来源  
使用多个 mixin ，property 来自哪个 mixin 变得不清晰。追溯实现和理解组件行为变得困难。

    > 使用 ref + 解构模式，property 的来源在消费组件时一目了然。

</v-click>

<div class="mt-10"></div>

<v-click>

- 命名空间冲突  
多个来自不同作者的 mixin 可能会注册相同的 property 键名。

    > 在解构变量时可以对变量进行重命名。

</v-click>

<div class="mt-10"></div>

<v-click>

- 隐式的跨 mixin 交流  
多个 mixin 需要依赖共享的 property 键名来进行相互作用，这使得它们隐性地耦合在一起。

    > 一个组合式函数的返回值可以作为另一个组合式函数的参数被传入，像普通函数那样。

</v-click>


---
clicks: 6
---

# 总结

<div class="grid grid-cols-2 gap-x-4 gap-y-4">

###### 对象式 存在的问题

###### 组合式 提供的能力

<v-clicks at="1">

- 上下文丢失
- 有限的类型支持
- 按 API 类型组织
- 不利于复用
- mixin 潜在命名冲突

</v-clicks>

<v-clicks at="1">

- 提供更好的上下文支持
- 更好的 TypeScript 类型支持
- 按功能/逻辑组织
- 极易复用 (原生 JS 函数)
- 可灵活组合 (生命周期钩子可多次使用)
- 可独立于 Vue 组件使用

</v-clicks>

</div>


---

# VueUse 是什么

Vue 组合式 API 工具包

<div class="mt-10 mb-10">
  <a class="!border-none" href="https://www.npmjs.com/package/@vueuse/core" target="__blank"><img class="h-4 inline mx-0.5" src="https://img.shields.io/npm/v/@vueuse/core?color=a1b858&label=" alt="NPM version"></a>
  <a class="!border-none" href="https://www.npmjs.com/package/@vueuse/core" target="__blank"><img class="h-4 inline mx-0.5" alt="NPM Downloads" src="https://img.shields.io/npm/dm/@vueuse/core?color=50a36f&label="></a>
  <img class="h-4 inline mx-0.5" alt="Function Count" src="https://img.shields.io/badge/-200+%20functions-13708a">
  <br>
</div>


  - 200+ 组合式函数
  - 同时兼容 Vue 2 和 Vue 3
  - Tree-shakeable
  - TypeScript
  - 丰富的扩展包，如 Router、Electron、RxJS
  - CDN 兼容
  - SSR 友好
  - 文档自带交互性演示


---
layout: center
class: text-center
---

# 实现一个 useMouse


---

# 命名

&nbsp;

约定用驼峰命名法命名，以 `use` 开头，如

- useLastChanged
- useLocalStorage
- useElementVisibility
- useWindowSize
- useDark
- useTitle
- useArrayMap
- useMouse


---

<div class="grid grid-cols-2 gap-x-4"><div>

# Ref

```ts
import { ref } from 'vue'
let foo = 0
let bar = ref(0)
foo = 1
bar = 1 // ts-error
```

<div class="mt-4" v-click>

###### 优点

- 显式调用，类型检查
- 相比 Reactive 局限更少

###### 缺点

- `.value`

</div>

</div><div>

# Reactive

```ts
import { reactive } from 'vue'
const foo = { prop: 0 }
const bar = reactive({ prop: 0 })
foo.prop = 1
bar.prop = 1
```

<div class="mt-4" v-click>

###### 优点

- 自动 Unwrap (即不需要 `.value`)

###### 缺点

- 在类型上和一般对象没有区别
- 使用 ES6 解构会使响应性丢失
- 需要使用箭头函数包装才能使用 `watch`

</div>
</div></div>

---

# 返回由 Ref 组成的对象 <MarkerPattern />

以在使用可组合的函数式，同时获得 `ref` 和 `reactive` 的好处。

<div class="mt-1" />
<div class="grid grid-cols-2 gap-x-4">
<v-clicks>

```ts
import { ref, reactive } from 'vue'
function useMouse() {
  const x = ref(0)
  const y = ref(0)
  return { x, y }
}
const { x, y } = useMouse()
const mouse = reactive(useMouse())
mouse.x === x.value // true
```

<div class="px-2 py-4">

- 可以直接使用 ES6 解构其中的 Ref 使用
- 根据使用方式，当想要自动解包的功能时，可以使用 `reactive` 将其转换为对象

</div>

</v-clicks>
</div>


---

# useMouse 简易实现

```ts
// mouse.js
import { ref, onMounted, onUnmounted } from 'vue'

export function useMouse() {      // 按照惯例，组合式函数名以 use 开头
  const x = ref(0)                // 被组合式函数封装和管理的状态
  const y = ref(0)

  function update(event) {         // 组合式函数可以随时更改其状态
    x.value = event.pageX
    y.value = event.pageY
  }
  // 一个组合式函数也可以挂靠在所属组件的生命周期上，来启动和卸载副作用
  onMounted(() => window.addEventListener('mousemove', update))
  onUnmounted(() => window.removeEventListener('mousemove', update))

  return { x, y }         // 通过返回值暴露所管理的状态
}
```


---

# 改进 - 副作用自动清除 <MarkerPattern />

一个组合式函数可以调用其他的组合式函数

```ts
// event.js
import { onMounted, onUnmounted } from 'vue'
export function useEventListener(target, event, callback) {
  onMounted(() => target.addEventListener(event, callback))
  onUnmounted(() => target.removeEventListener(event, callback))
}
```
```ts
// mouse.js
import { ref } from 'vue'
import { useEventListener } from './event'
export function useMouse() {
  const x = ref(0)
  const y = ref(0)
  useEventListener(window, 'mousemove', (event) => {
    x.value = event.pageX
    y.value = event.pageY
  })

  return { x, y }
}
```


---

# 使用

```html
<script setup>
import { useMouse } from './mouse.js'

const { x, y } = useMouse()
</script>

<template>鼠标的位置在 {{ x }}, {{ y }}</template>
```

<DemoMouse />


---

# 改进 - 节流防抖 <MarkerPattern />

```ts {maxHeight:'100'}
function debounceFilter(ms: number) {
  let timer
  const filter = (invoke) => {
    const duration = unref(ms)
    if (timer) clearTimeout(timer)
    if (duration <= 0) { return invoke() }
    timer = setTimeout(() => { invoke() }, duration)
  }
  return filter
}
function useMouse(options: useMouseOption = {}) {
  const { eventFilter } = options
  const mouseHandler = (event: MouseEvent) => {
    x.value = event.pageX
    y.value = event.pageY
  }
  const mouseHandlerWrapper = (event: MouseEvent) => {
    return eventFilter === undefined ? mouseHandler(event) : eventFilter(() => mouseHandler(event))
  }
  useEventListener(window, 'mousemove', mouseHandlerWrapper)
```


---

# 使用

```html
<script setup>
import { useMouse } from './mouse2.js'

const { x, y } = useMouse({ eventFilter: debounceFilter(200) })
</script>

<template>鼠标的位置在 {{ x }}, {{ y }}</template>
```

<DemoMouse2 />


---

<DemoMouse3 />


---
layout: center
class: text-center
---

# 实现一个 useTitle


---

# Ref 自动解包 <MarkerCore />

在众多情况下，我们可以减少 `.value` 的使用

<div class="grid grid-cols-[320px,1fr] gap-x-4 gap-y-2 pt-4">

<v-clicks :every='2'>

- `watch` 直接接受 Ref 作为监听对象，并在回调函数中返回解包后的值

```ts
const counter = ref(0)
watch(counter, count => {
  console.log(count) // 同 `counter.value`
})
```

- Ref 在模版中自动解包

```html
<template>
  <button @click="counter += 1">
    Counter is {{ counter }}
  </button>
</template>
```

- 使用 Reactive 解包嵌套的 Ref

<div>

```ts
import { ref, reactive } from 'vue'
const foo = ref('bar')
const data = reactive({ foo, id: 10 })
data.foo // 'bar'
```

</div>

</v-clicks>

</div>

---

# 重复使用已有 Ref <MarkerCore />

如果将一个 `ref` 传递给 `ref()` 构造函数，它将会原样将其返回。

<v-clicks>

```ts
const foo = ref(1)   // Ref<1>
const bar = ref(foo) // Ref<1>

foo === bar // true
```

```ts
function useFoo(foo: Ref<string> | string) {
  const bar = isRef(foo) ? foo : ref(foo)
  // 等效于
  const bar = ref(foo)
}
```

这个技巧在编写不确定参数类型的函数时十分有用。

</v-clicks>

---

# `unref` - Ref 的反操作 <MarkerCore />

- 如果传入一个 Ref ，返回其值
- 否则原样返回

<div class="grid grid-cols-2 gap-x-4 mt-4">

<div v-click>

###### 实现

```ts
function unref<T>(r: Ref<T> | T): T {
  return isRef(r) ? r.value : r
}
```

</div><div v-click>

###### 使用

```ts
import { unref, ref } from 'vue'
const foo = ref('foo')
unref(foo) // 'foo'
const bar = 'bar'
unref(bar) // 'bar'
```

</div></div>

---

# 接受 Ref 作为函数参数 <MarkerPattern />

<div class="grid grid-cols-[160px,1fr,220px] gap-x-4">

<div />

###### 实现

###### 用例

<v-clicks :every='3'>

<div class="my-auto leading-6 text-base opacity-75">
纯函数
</div>


```ts
function add(a: number, b: number) {
  return a + b
}
```

```ts
let a = 1
let b = 2
let c = add(a, b) // 3
```

<div class="my-auto leading-6 text-base opacity-75">
接受 Ref 作为参数，<br>
返回一个响应式的结果
</div>

```ts
function add(a: Ref<number>, b: Ref<number>) {
  return computed(() => a.value + b.value)
}
```

```ts
const a = ref(1)
const b = ref(2)
const c = add(a, b)
c.value // 3
```

<div class="my-auto leading-6 text-base opacity-75">
同时接受传入值和 Ref
</div>

```ts
function add(
  a: Ref<number> | number,
  b: Ref<number> | number
) {
  return computed(() => unref(a) + unref(b))
}
```

```ts
const a = ref(1)
const c = add(a, 5)
c.value // 6
```

</v-clicks>

</div>

---

# MaybeRef 类型工具 <MarkerTips/>

```ts
type MaybeRef<T> = Ref<T> | T
```

可选择性的响应式参数。

```ts
import { computed, unref, Ref } from 'vue'
type MaybeRef<T> = Ref<T> | T
export function useTimeAgo(
  // time: Date | number | string | Ref<Date | number | string>,
  time: MaybeRef<Date | number | string>,
) {
  return computed(() => someFormating(unref(time)))
}
```

---

# 小结

<div v-click>

- `MaybeRef<T>` 可以很好的配合 `ref` 和 `unref` 进行使用。
- 使用 `ref()` 当你想要想要将其标准化为 Ref
- 使用 `unref()` 当你想要获得其值

<br>

```ts
type MaybeRef<T> = Ref<T> | T
function useBala<T>(arg: MaybeRef<T>) {
  const reference = ref(arg) // 得到 ref
  const value = unref(arg)   // 得到值
}
```

</div>


---

# useTitle 简易实现

<div class="grid grid-cols-[450px,1fr] gap-4">


```ts
import { ref, watch } from 'vue'
type MaybeRef<T> = Ref<T> | T

export function useTitle(
  newTitle: MaybeRef<string | null | undefined>
) {
  const title = ref(newTitle || document.title)

  watch(title, (t) => {
    if (t != null)
      document.title = t
  }, { immediate: true })

  return title
}
```

<v-click>

```html






<-- 1. 重复使用用户提供的 Ref, 或者建立一个新的

<-- 2. 将页面标题与 Ref 进行同步



```

</v-click>
</div>


---

# useTitle 使用

```html
<script setup lang="ts">
import { useTitle } from './useTitle'
const title = useTitle(null)
</script>

<template>
  <span class="mr-5">修改title：</span>
  <input class="mt-10 border" v-model="title" type="text">
</template>
```

<DemoTitle />


---
layout: center
class: text-center
---

# 实现一个 useDark


---

# 为更好的代码组织抽取组合式函数 <MarkerPattern />

&nbsp;

抽取组合式函数不仅是为了复用，也是为了代码组织。  
随着组件复杂度的增高，可能会最终发现组件多得难以查询和理解。

通过组合式，可以基于逻辑问题将组件代码拆分成更小的函数：

```html
<script setup>
import { useFeatureA } from './featureA.js'
import { useFeatureB } from './featureB.js'
import { useFeatureC } from './featureC.js'

const { foo, bar } = useFeatureA()
const { baz } = useFeatureB(foo)
const { qux } = useFeatureC(baz)
</script>
```


---

# 简易实现

```ts {all|3,4|all}
import { usePreferredDark, useColorMode } from '@vueuse/core'
export function useDark() {
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
```


---

# 使用

```html {all|3,6|all}
<script setup lang="ts">
import { useDark } from './useDark.ts'
import { useToggle } from '@vueuse/core'

const isDark = useDark()
const toggleDark = useToggle(isDark)
</script>
<template>
  <button
    @click="toggleDark()">
    <carbon:moon v-if="isDark" />
    <carbon:sun v-else />

    <span class="mr-1 ml-2">{{ isDark ? 'Dark' : 'Light' }}</span>
  </button>
</template>
```

<DemoDark />


---

# 组合关系

&nbsp;

```mermaid {theme:'dark'}
graph LR;
    useToggle-->useDark;
    useDark{{useDark}}-->usePreferredDark;
    usePreferredDark-->useMediaQuery;
    useMediaQuery-->useSupported;
    useDark-->useColorMode;
    useColorMode{{useColorMode}}-->useStorage;
    useColorMode-->usePreferredDark;
    useStorage-->useEventListener;
```

<div class="mt-10">

- 其中每一个函数都可以独立使用
- 专注点分离

</div>


---


# 建立"连结" <MarkerPattern />

Vue 的 `setup()` 只会在组件建立时执行**一次**，并建立数据与逻辑之间的连结。

- 建立 输入 → 输出 的连结

- 输出会自动根据输入的改变而改变

<div class="grid grid-cols-[auto,1fr] gap-4">
  <div v-click class="p-4">
    <h3 class="pb-2">Excel 中的公式</h3>
    <img class="h-40" src="https://cdn.wallstreetmojo.com/wp-content/uploads/2019/01/Division-Formula-in-Excel-Example-1-1.png">
  </div>
</div>


---
layout: center
class: text-center
---

# 实现一个 useFetch


---

# 使用 shallowRef

&nbsp;

和 `ref()` 不同，浅层 ref 的内部值将会原样存储和暴露，  
不会被深层递归地转为响应式。  
对 .value 的访问是响应式的。


---

# useFetch 简易实现

```ts
export function useFetch<R>(url: MaybeRef<string>) {
  const data = shallowRef<T | undefined>()
  const error = shallowRef<Error | undefined>()
  fetch(unref(url))
    .then(r => r.json())
    .then(r => data.value = r)
    .catch(e => error.value = e)
  return {
    data,
    error
  }
}
```


---

# 将异步操作转换为 同步 <MarkerTips />

将异步请求转换为 **同步** 的

<div v-click>

###### 异步

```ts
const data = await fetch('https://api.github.com/').then(r => r.json())
// use data
```

</div>
<div v-click>

###### useFetch

```ts
const { data } = useFetch('https://api.github.com/').json()
const user_url = computed(() => data.value?.user_url)
```

</div>
<div v-click> 

先建立数据间的 连结 ，然后再等待异步请求返回将数据填充。

</div>


---
layout: center
---

# 总结

- 返回由 Ref 组成的对象
- 副作用自动清除
- 接受 Ref 作为函数参数
- 使用 ref / unref / MaybeRef
- 抽离组合式函数
- 建立 “连结”
- 大量数据使用 shallowRef
- 将异步操作转换为 同步


---

<LastSummary />


---
layout: center
---

# 谢谢


---

<ScrollTimeline />

