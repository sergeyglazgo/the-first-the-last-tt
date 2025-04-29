<template>
  <div class="home-content">
    <h1 ref="title" class="home-content__title">
      FULL-CYCLE
      <span class="home-content__title-part">
        <span class="home-content__word">EVENT </span>
        <span class="home-content__word">AGENCY</span>
      </span>
    </h1>
    <RotatingShowreel />
  </div>
</template>

<script setup>
import { ref, onBeforeUnmount, onMounted } from 'vue'
import RotatingShowreel from './RotatingShowreel.vue'

const title = ref(null)

function handleMouseMove(event) {
  if (!title.value) return

  const { clientX, clientY } = event
  const windowWidth = window.innerWidth
  const windowHeight = window.innerHeight

  const offsetX = ((clientX / windowWidth) - 0.5) * 20
  const offsetY = ((clientY / windowHeight) - 0.5) * 20

  title.value.style.transform = `translate(${offsetX}px, ${offsetY}px)`
}

onMounted(() => {
  window.addEventListener('mousemove', handleMouseMove)
})

onBeforeUnmount(() => {
  window.removeEventListener('mousemove', handleMouseMove)
})
</script>

<style scoped lang="scss">
.home-content {
  position: relative;
  text-align: center;

  &::before {
    content: '';
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 320px;
    aspect-ratio: 1;
    border-radius: 50%;
    background: radial-gradient(
        circle,
        rgba($color-yellow, 1) 50%,
        rgba($color-yellow, 0) 70%
    );
    z-index: -1;
  }

  &__title {
    font-size: 34px;
    font-family: 'GrtskGiga-Bold', sans-serif;
    line-height: 1.1;
  }

  &__title-part,
  &__word {
    display: block;
  }
}

@media (min-width: $tablet) {
  .home-content {
    &::before {
      width: 520px;
    }

    &__title {
      font-size: 58px;
    }

    &__word {
      display: inline;
    }
  }
}

@media (min-width: $desktop) {
  .home-content {
    &::before {
      width: 630px;
    }

    &__title {
      font-size: 82px;
    }
  }
}
</style>
