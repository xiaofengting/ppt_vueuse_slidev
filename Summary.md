
# 一、状态

1. `createGlobalState`： 创建全局状态
2. `createInjectionState`： 创建可以注入组件的全局状态
3. `createSharedComposable`： 重用可组合函数之前的状态
4. `useAsyncState`： 异步状态
5. `useLastChanged`： 记录上次更改的时间戳
6. `useRefHistory`： 跟踪 ref 的更改历史
7. `useManualRefHistory`： 手动跟踪更改历史
8. `useDebouncedRefHistory`： 带防抖的 useRefHistory
9. `useThrottledRefHistory`： 带节流的 useRefHistory
10. `useStorage`： localStorage 或 SessionStorage
11. `useStorageAsync`： 异步支持的 useStorage
12. `useLocalStorage`： localStorage
13. `useSessionStorage`： SessionStorage


# 二、元素

1. `useActiveElement`： document.activeElement
2. `useDocumentVisibility`： document.visibilityState
3. `useDraggable`： 使元素可拖动
4. `useDropZone`： 创建一个可以放置的区域
5. `useElementBounding`： 元素的边界框
6. `useElementSize`： 元素宽高 ResizeObserver
7. `useElementVisibility`： 元素在视口内可见性
8. `useIntersectionObserver`： 元素的可见性
9. `useMouseInElement`： 光标在元素内的位置
10. `useMutationObserver`： DOM 树的变化 MutationObserver
11. `useResizeObserver`： 元素宽高 ResizeObserver
12. `useWindowFocus`： 窗口聚焦
13. `useWindowScroll`： 窗口滚动
14. `useWindowSize`： 窗口大小


# 三、浏览器

1. `useBluetooth`： 蓝牙 Bluetooth API
2. `useBreakpoints`： 视口断点
3. `useBroadcastChannel`： 广播 BroadcastChannel API
4. `useBrowserLocation`： 浏览器 location
5. `useClipboard`： 剪贴板 Clipboard API
6. `useColorMode`： 颜色模式
7. `useCssVar`： 操作 CSS 变量
8. `useDark`： 暗黑模式
9. `useEventListener`： EventListener
10. `useEyeDropper`： 吸管 EyeDropper API
11. `useFavicon`： 网站图标 favicon
12. `useFileDialog`： 文件对话框
13. `useFileSystemAccess`： 文件系统访问 File System Access API
14. `useFullscreen`： 全屏 Fullscreen API
15. `useGamepad`： 游戏手柄 Gamepad API
16. `useImage`： 图像
17. `useMediaControls`： audio 和 video 的媒体控制
18. `useMediaQuery`： 媒体查询
19. `useMemory`： 内存信息
20. `useObjectUrl`： URL 对象
21. `usePermission`： 权限 Permissions API
22. `usePreferredColorScheme`： 用户偏好颜色模式
23. `usePreferredContrast`： 用户偏好对比度
24. `usePreferredDark`： 用户偏好暗黑模式
25. `usePreferredLanguages`： 用户首选语言 Navigator.languages
26. `usePreferredReducedMotion`： 屏幕方向 Screen Orientation API
27. `useScreenOrientation`： 屏幕方向 Screen Orientation API
28. `useScreenSafeArea`： 屏幕安全区域
29. `useScriptTag`： 脚本标签
30. `useShare`： 共享 Share API
31. `useStyleTag`： 注入样式标签
32. `useTextareaAutosize`： 自动更新文本区域的高度
33. `useTextDirection`： 文本方向
34. `useTitle`： 网页标题 document.title
35. `useUrlSearchParams`： URL 查询字符串
36. `useVibrate`： 振动 Vibration API
37. `useWakeLock`： 屏幕唤醒锁 Screen Wake Lock API
38. `useWebNotification`： 通知 Notifications API
39. `useWebWorker`： Web Workers
40. `useWebWorkerFn`： Web Worker 运行函数


# 四、传感器

1. `onClickOutside`： 元素外部的点击
2. `onKeyStroke`： 键盘点击
3. `onLongPress`： 长按
4. `onStartTyping`： 开始打字
5. `useBattery`： 电池电量 Battery Status API
6. `useDeviceMotion`： 设备位置方向的改变 DeviceMotionEvent
7. `useDeviceOrientation`： 设备的物理方向 DeviceOrientationEvent
8. `useDevicePixelRatio`： 设备像素比 devicePixelRatio
9. `useDevicesList`： 媒体输入和输出设备的列表
10. `useDisplayMedia`： 屏幕捕获 getDisplayMedia
11. `useElementByPoint`： 根据点获取元素
12. `useElementHover`： 元素的悬浮状态
13. `useFocus`： 聚焦
14. `useFocusWithin`： 元素或后代之一是否具有焦点
15. `useFps`： FPS
16. `useGeolocation`： 地理位置 Geolocation API
17. `useIdle`： 用户是否处于非活动状态
18. `useInfiniteScroll`： 无限滚动元素
19. `useKeyModifier`： 修饰键状态
20. `useMagicKeys`： 按键组合
21. `useMouse`： 光标位置
22. `useMousePressed`： 鼠标按下状态
23. `useNavigatorLanguage`： 用户偏好语言 Navigator.language
24. `useNetwork`： 网络状况 Network Information API
25. `useOnline`： 网络连接状态
26. `usePageLeave`： 光标是否离开页面
27. `useParallax`： 创建视差效果
28. `usePointer`： 指针状态
29. `usePointerSwipe`： 指针滑动
30. `useScroll`： 滚动位置和状态
31. `useScrollLock`： 锁定元素的滚动
32. `useSpeechRecognition`： 语音识别 Speech API
33. `useSpeechSynthesis`： 语音合成
34. `useSwipe`： touch 滑动
35. `useTextSelection`： 文本选择 Window.getSelection()
36. `useUserMedia`： 媒体输入


# 五、网络

1. `useEventSource`： 服务器推送的一个网络事件接口
2. `useFetch`： 请求 Fetch API
3. `useWebSocket`： WebSocket 客户端


# 六、动画

1. `useInterval`： setInterval
2. `useIntervalFn`： setInterval
3. `useNow`： 当前 Date
4. `useRafFn`： requestAnimationFrame
5. `useTimeout`： setTimeout
6. `useTimeoutFn`： setTimeout
7. `useTimestamp`： 当前时间戳
8. `useTransition`： 过渡


# 七、组件

1. `computedInject`： 结合 computed 和 inject
2. `templateRef`： 模板元素的ref
3. `tryOnBeforeMount`： 安全的 onBeforeMount
4. `tryOnBeforeUnmount`： 安全的 onBeforeUnmount
5. `tryOnMounted`： 安全的 onMounted
6. `tryOnScopeDispose`： 安全的 onScopeDispose
7. `tryOnUnmounted`： 安全的 onUnmounted
8. `unrefElement`： DOM 元素的解包
9. `useCurrentElement`： 获取当前组件的 DOM 元素作为 ref
10. `useMounted`： 挂载状态
11. `useTemplateRefsList`： v-for 绑定 ref
12. `useVirtualList`： 虚拟列表
13. `useVModel`： v-model 绑定的简写
14. `useVModels`： v-model 绑定的简写


# 八、watch

1. `until`： 直到...触发一次
2. `watchArray`： 数组增加、删除的元素
3. `watchAtMost`： 限制次数的 watch
4. `watchDebounced`： 防抖的 watch
5. `watchThrottled`： 节流的 watch
6. `watchIgnorable`： 有忽略功能的 watch
7. `watchOnce`： 只触发一次
8. `watchPausable`： 可暂停的 watch
9. `watchTriggerable`： 可手动触发的 watch
10. `watchWithFilter`： 有 eventFilter 的 watch
11. `whenever`： truthy 触发的 watch


# 九、响应式

1. `computedAsync`： 异步函数的 computed
2. `computedEager`： 无惰性求值的 computed
3. `computedWithControl`： 明确依赖的 computed
4. `extendRef`： 为 Ref 添加额外属性
5. `reactify`： 将普通函数转换为响应式函数
6. `reactifyObject`： 用于对象的 reactify
7. `reactiveComputed`： 返回 reactive 的 computed
8. `reactiveOmit`： 忽略部分字段的 reactive
9. `reactivePick`： 选择部分字段的 reactive
10. `refAutoReset`： 一段时间后恢复默认值的 ref
11. `refDebounced`： 防抖的 ref
12. `refThrottled`： 节流的 ref
13. `refDefault`： 带默认值的 ref
14. `refWithControl`： 细粒度控制的 ref
15. `resolveRef`： 规范化的 ref
16. `resolveUnref`： 规范化的 unref
17. `syncRef`： 双向同步 ref
18. `syncRefs`： 同步 refs
19. `toReactive`： ref 转 reactive
20. `toRefs`： 接收对象引用的 toRefs


# 十、数组

1. `useArrayEvery`： Array.every
2. `useArrayFilter`： Array.filter
3. `useArrayFind`： Array.find
4. `useArrayFindIndex`： Array.findIndex
5. `useArrayJoin`： Array.join
6. `useArrayMap`： Array.map
7. `useArrayReduce`： Array.reduce
8. `useArraySome`： Array.some


# 十一、时间

1. `useDateFormat`： 格式化日期
2. `useTimeAgo`： 多久之前


# 十二、实用

1. `createEventHook`： 事件钩子
2. `createUnrefFn`： 参数自动解包的函数
3. `get`： ref.value
4. `set`： ref.value = x
5. `isDefined`： 是否已定义
6. `makeDestructurable`： 对象和数组同构
7. `useAsyncQueue`： 顺序执行异步队列
8. `useBase64`： base64 转换
9. `useCached`： 缓存
10. `useConfirmDialog`： 创建对话框
11. `useCounter`： 计数器
12. `useCycleList`： 循环列表
13. `useDebounceFn`： 函数防抖
14. `useThrottleFn`： 函数节流
15. `useEventBus`： 事件总线
16. `useMemoize`： 缓存
17. `useOffsetPagination`： 分页
18. `useStepper`： 步进器
19. `useSupported`： 是否支持
20. `useTimeoutPoll`： 使用 timeout 轮询
21. `useToggle`： 布尔值切换
22. `useToNumber`： ref 转 number
23. `useToString`： ref 转 string


# 十三、数学

1. `createGenericProjection`： 通用投影
2. `createProjection`： 数学投影
3. `logicAnd`： 与
4. `logicNot`： 非
5. `logicOr`： 或
6. `useAbs`： Math.abs
7. `useAverage`： 平均值
8. `useCeil`： Math.ceil
9. `useClamp`： 两个值之间的值
10. `useFloor`： Math.floor
11. `useMath`： Math
12. `useMax`： Math.max
13. `useMin`： Math.min
14. `usePrecision`： 精度
15. `useProjection`： 投影
16. `useRound`： Math.round
17. `useSum`： 求和
18. `useTrunc`： Math.trunc


# 十四、Router

1. `useRouteHash`： route.hash
2. `useRouteParams`： route.params
3. `useRouteQuery`： route.query


# 十五、结合其他包

1. `useAsyncValidator`： async-validator
2. `useAxios`： axios
3. `useChangeCase`： change-case
4. `useCookies`： universal-cookie
5. `useDrauu`： drauu
6. `useFocusTrap`： focus-trap
7. `useFuse`： fuse.js
8. `useJwt`： jwt-decode
9. `useNProgress`： nprogress
10. `useQRCode`： qrcode

