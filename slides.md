---
theme: default
title: Vue 3
highlighter: shiki
---

# 可组合的 Vue

学习 VueUse ，
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

# 组合式

---
clicks: 4
---

# 什么是组合式 API ？

在 Vue 3 中引入的一种新的编写 Vue 组件的方式。

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
clicks: 2
---

# 什么是组合式函数 ？

利用 Vue 组合式 API 来封装和复用有状态逻辑的函数。

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
import { ref, computed } from 'vue'
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

# 组合式的优势

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
  <a class="!border-none" href="https://vueuse.org" target="__blank"><img class="h-4 inline mx-0.5" src="https://img.shields.io/static/v1?label=&message=docs%20%26%20demos&color=1e8a7a" alt="Docs & Demos"></a>
  <img class="h-4 inline mx-0.5" alt="Function Count" src="https://img.shields.io/badge/-114%20functions-13708a">
  <br>
</div>


  - 同时兼容 Vue 2 和 Vue 3
  - Tree-shakeable ESM
  - TypeScript
  - CDN 兼容
  - 核心包含 110+ 组合式函数
  - 丰富的生态系统 8+ 扩展包

---
layout: center
class: text-center
---

# useTitle

---

# 使用

```html
<script setup lang="ts">
import { useTitle } from '@vueuse/core'
const title = useTitle(null)
</script>

<template>
  <span class="mr-5">修改title：</span>
  <input class="mt-10 border" v-model="title" type="text">
</template>
```

<DemoTitle />

---

# 简易实现

<div class="grid grid-cols-[450px,1fr] gap-4">


```ts
import { ref, watch } from 'vue'
import type { MaybeRef } from '@vueuse/shared'

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

# 再看一遍

<div class="grid grid-cols-[450px,1fr] gap-4">

```ts
import { ref, watch } from 'vue'
import type { MaybeRef } from '@vueuse/shared'

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

```html






<-- 1. 重复使用用户提供的 Ref, 或者建立一个新的

<-- 2. 将页面标题与 Ref 进行同步



```

</div>

---
layout: center
class: text-center
---

# useMouse

---

```ts
import { useMouse } from '@vueuse/core'

const { x, y, sourceType } = useMouse()
```








---
layout: center
class: text-center
---

# useDark

---


---

---

# useFullscreen


---

# useImage


