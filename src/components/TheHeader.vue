<template>
  <header class="site-header">
    <LanguageSelector class="site-header__language-selector" />
    <TheLogo class="site-header__logo" />
    <BurgerMenu class="site-header__burger-menu" />
  </header>
</template>

<script setup>
import TheLogo from '@/components/TheLogo.vue'
import LanguageSelector from './LanguageSelector.vue'
import BurgerMenu from '@/components/BurgerMenu.vue'
</script>

<style scoped lang="scss">
.site-header {
  width: 100vw;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem;
  position: fixed;
  z-index: 100;

  &__language-selector {
    position: relative;
    z-index: 1;
  }

  &__logo {
    position: absolute;
    left: 50%;
    transform: translateX(-50%);
  }
}
</style>
