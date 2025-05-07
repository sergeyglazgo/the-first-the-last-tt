<template>
  <img
    class="rotating-showreel"
    src="/showreel.svg"
    role="presentation"
  >
</template>

<style scoped lang="scss">
.rotating-showreel {
  position: absolute;
  bottom: -100px;
  right: 50px;
  cursor: pointer;
  transition: transform 0.1s linear;
  animation: rotate 5s linear infinite;
  animation-play-state: paused;

  &:hover {
    animation-play-state: running;
  }

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
