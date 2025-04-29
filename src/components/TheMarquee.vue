<template>
  <div
    class="marquee"
    :style="{ transform: `rotate(-${dynamicAngle}deg)` }"
  >
    <div
      class="marquee__row"
      v-for="(row, index) in rows"
      :key="index"
      :class="{
        'marquee__row--reverse': index % 2 === 1,
        'marquee__row--flipped': index === 0
      }"
    >
      <div class="marquee__content">
        <span
          class="marquee__text"
          v-for="(_, i) in 20"
          :key="i"
        >
          {{ row }}
        </span>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const rows = ['EVENT AGENCY', 'EVENT AGENCY']
const dynamicAngle = ref(45)

const updateAngle = () => {
  const viewportWidth = window.innerWidth
  const viewportHeight = window.innerHeight

  if (viewportWidth === 0) return

  const angleInRadians = Math.atan(viewportHeight / viewportWidth)
  dynamicAngle.value = angleInRadians * (180 / Math.PI)
}

onMounted(() => {
  updateAngle()
  window.addEventListener('resize', updateAngle)
})

onUnmounted(() => {
  window.removeEventListener('resize', updateAngle)
})
</script>

<style scoped lang="scss">
.marquee {
  position: absolute;
  bottom: -70px;
  left: 0;
  width: 300%;
  overflow: hidden;
  z-index: -2;
  transform-origin: bottom left;

  &__row {
    display: flex;
    margin: 4px 0;
    white-space: nowrap;
    overflow: hidden;
    width: 100%;
    transform: skewX(-20deg);

    &--reverse .marquee__content {
      animation-direction: reverse;
    }

    &--flipped .marquee__text {
      transform: scale(-1);
    }
  }

  &__content {
    display: inline-flex;
    animation: marquee 70s linear infinite;
    will-change: transform;
  }

  &__text {
    display: inline-block;
    padding: 0 10px;
    font-size: 28px;
    font-family: 'GrtskGiga-Bold', sans-serif;
    color: transparent;
    -webkit-text-stroke: 1px rgba(0, 0, 0, 0.1);
    text-transform: uppercase;
  }
}

@media (min-width: 480px) {
  .marquee {
    &__text {
      font-size: 42px;
      padding: 0 15px;
    }
  }
}

@media (min-width: 768px) {
  .marquee {
    &__text {
      font-size: 52px;
      padding: 0 20px;
    }
  }
}

@keyframes marquee {
  0% {
    transform: translate3d(0, 0, 0);
  }
  100% {
    transform: translate3d(-50%, 0, 0);
  }
}
</style>
