<template>
  <img
    class="rotating-showreel"
    :style="{ transform: `rotate(-${rotationAngle}deg)` }"
    src="/showreel.svg"
    alt=""
    @mouseover="startRotation"
    @mouseout="stopRotation"
  >
</template>

<script setup>
import { ref } from 'vue'

const rotationAngle = ref(0)
let animationFrameId = null
let lastTimestamp = null
let isRotating = false

const rotateStep = (timestamp) => {
  if (!lastTimestamp) lastTimestamp = timestamp
  const delta = timestamp - lastTimestamp
  lastTimestamp = timestamp

  // 70 deg/sec
  rotationAngle.value += (delta / 1000) * 70

  if (isRotating) {
    animationFrameId = requestAnimationFrame(rotateStep)
  }
}

const startRotation = () => {
  if (!isRotating) {
    isRotating = true
    lastTimestamp = null
    animationFrameId = requestAnimationFrame(rotateStep)
  }
}

const stopRotation = () => {
  isRotating = false
  cancelAnimationFrame(animationFrameId)
  animationFrameId = null
}
</script>

<style scoped lang="scss">
.rotating-showreel {
  position: absolute;
  bottom: -100px;
  right: 50px;
  cursor: pointer;
  transition: transform 0.1s linear;

  @media (min-width: $tablet) {
    width: 112px;
    height: 112px;
    bottom: -150px;
    right: 140px;
  }

  @media (min-width: $desktop) {
    width: 118px;
    height: 118px;
    right: 240px;
  }
}

@keyframes rotate {
  from {
    transform: rotate(360deg);
  }
  to {
    transform: rotate(0deg);
  }
}
</style>
