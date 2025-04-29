<template>
  <div class="home-container">
    <HomeContent />
    <TheNavigation class="navigation" />
    <TheMarquee />
  </div>
</template>

<script setup>
import HomeContent from '@/components/HomeContent.vue'
import TheNavigation from '@/components/TheNavigation.vue'
import TheMarquee from '@/components/TheMarquee.vue'
</script>

<style scoped lang="scss">
.home-container {
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
  overflow: hidden;
}

@media (max-width: $mobile) {
  .navigation {
    display: none;
  }
}
</style>
