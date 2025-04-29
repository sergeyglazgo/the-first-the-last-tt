<template>
  <div class="app">
    <TheHeader />
    <router-view v-slot="{ Component, route }">
      <transition
        name="page-wipe"
        mode="out-in"
        @before-leave="onBeforeLeave"
        @leave="onLeave"
        @enter="onEnter"
        @after-enter="onAfterEnter"
      >
        <component :is="Component" :key="route.path" />
      </transition>
    </router-view>

    <div ref="overlay" class="page-transition-overlay"></div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import TheHeader from '@/components/TheHeader.vue'

const overlay = ref(null)

const animationDuration = 400
const easing = 'cubic-bezier(0.65, 0, 0.35, 1)'

const onBeforeLeave = () => {
  if (overlay.value) {
    overlay.value.style.transition = 'none'
    overlay.value.style.transform = 'translateX(-101%) skewX(15deg)'
  }
}

const onLeave = (el, done) => {
  if (overlay.value) {
    overlay.value.style.transition = `transform ${animationDuration}ms ${easing}`
    overlay.value.style.transform = 'translateX(0)'
  }
  setTimeout(done, animationDuration)
};

const onEnter = (el, done) => {
  if (overlay.value) {
    overlay.value.style.transition = `transform ${animationDuration}ms ${easing}`
    overlay.value.style.transform = 'translateX(101%)'
  }
  setTimeout(done, animationDuration);
};

const onAfterEnter = () => {
  if (overlay.value) {
    overlay.value.style.pointerEvents = 'none'
  }
}
</script>

<style lang="scss">
.app {
  width: 100vw;
  height: 100vh;
  position: relative;
  overflow: hidden;
}

.page-transition-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: $color-yellow;
  transform: translateX(-101%);
  z-index: 1000;
  pointer-events: none;
}
</style>
