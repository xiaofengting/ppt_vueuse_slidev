
<template>
  <main id="main">
    <section class="red" id="section_1">
      <div class="panelwrapper">
        <div class="panel panel--left">
          <h1>useStorage</h1>
        </div>
        <div class="panel panel--right">
          <h3>响应式的 LocalStorage、SessionStorage</h3>
        </div>
      </div>
    </section>
    <section class="orange" id="section_2">
      <div class="panelwrapper">
        <div class="panel panel--left">
          <h1>useImage</h1>
        </div>
        <div class="panel panel--right">
          <h3>响应式加载图像</h3>
        </div>
      </div>
    </section>
    <section class="yellow" id="section_3">
      <div class="panelwrapper">
        <div class="panel panel--left">
          <h1>useStyleTag</h1>
        </div>
        <div class="panel panel--right">
          <h3>插入响应式的 style 标签</h3>
        </div>
      </div>
    </section>
    <section class="green" id="section_4">
      <div class="panelwrapper">
        <div class="panel panel--left">
          <h1>useArrayMap</h1>
        </div>
        <div class="panel panel--right">
          <h3>响应式的 Array.map</h3>
        </div>
      </div>
    </section>
  </main>
</template>

<style scoped>
main {
  height: 100%;
  scroll-snap-type: y mandatory;
  overflow-x: hidden;
  color: #323232;
}

main h1 {
  font-size: 4em;
}

section {
  height: 99%;
  width: 100%;
  scroll-snap-align: center;
  position: sticky;
  top: 0;
}

.panelwrapper {
  height: 100%;
  width: 100%;
  position: relative;
}

.red .panel {
  background: #f44336;
}

.orange .panel {
  background: #ff9800;
}

.yellow .panel {
  background: #ffd600;
}

.green .panel {
  background: #4caf50;
}

.panel {
  height: 100%;
  top: 0;
  position: absolute;
  padding: 4em;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.panel--left,
.panel--right {
  width: 50%;
}

.panel--left {
  left: 0;
}

.panel--right {
  right: 0;
}

@supports (animation-timeline: works) {
  @keyframes shrink-to-back {
    from {
      transform: scale(1);
    }

    to {
      transform: scale(0.5);
    }
  }

  @keyframes slide-in-from-left {
    from {
      transform: translateX(-100%) translateY(-100%);
      box-shadow: 0 0 1em hsl(0deg 0% 0% / 0.5);
    }

    to {
      transform: translateX(0) translateY(0%);
      box-shadow: 0 0 1em hsl(0deg 0% 0% / 0);
    }
  }

  @keyframes slide-in-from-right {
    from {
      transform: translateX(100%) translateY(-100%);
      box-shadow: 0 0 1em hsl(0deg 0% 0% / 0.5);
    }

    to {
      transform: translateX(0) translateY(0%);
      box-shadow: 0 0 1em hsl(0deg 0% 0% / 0);
    }
  }

  .panelwrapper {
    transform-origin: 50% 50%;
    animation: shrink-to-back 10s linear both;
    animation-timeline: foo;
  }

  .panel--left {
    animation: slide-in-from-left 10s linear both;
    animation-timeline: foo;
  }

  .panel--right {
    animation: slide-in-from-right 10s linear both;
    animation-timeline: foo;
  }

  @scroll-timeline section_2_slides_into_wrapper {
    source: selector(#main);
    scroll-offsets: selector(#section_2) end 0, selector(#section_2) end 1;
    start: selector(#section_2) end 0;
    end: selector(#section_2) end 1;
    time-range: 10s;
  }

  #section_1 .panelwrapper,
  #section_2 .panel {
    animation-timeline: section_2_slides_into_wrapper;
  }

  @scroll-timeline section_3_slides_into_wrapper {
    source: selector(#main);
    scroll-offsets: selector(#section_3) end 0, selector(#section_3) end 1;
    start: selector(#section_3) end 0;
    end: selector(#section_3) end 1;
    time-range: 10s;
  }

  #section_2 .panelwrapper,
  #section_3 .panel {
    animation-timeline: section_3_slides_into_wrapper;
  }

  @scroll-timeline section_4_slides_into_wrapper {
    source: selector(#main);
    scroll-offsets: selector(#section_4) end 0, selector(#section_4) end 1;
    start: selector(#section_4) end 0;
    end: selector(#section_4) end 1;
    time-range: 10s;
  }

  #section_3 .panelwrapper,
  #section_4 .panel {
    animation-timeline: section_4_slides_into_wrapper;
  }
}
</style>