<template>
  <div class="burger-menu-container">
    <div
      class="burger-menu"
      :class="{ 'burger-menu--open menu--active': showMenu }"
      @click="showMenu = !showMenu"
    >
      <span class="burger-menu__line"></span>
      <span class="burger-menu__line"></span>
    </div>
    <TheNavigation
      v-show="showMenu"
      class="navigation"
      @close="showMenu = false"
    />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import TheNavigation from '@/components/TheNavigation.vue'

const showMenu = ref(false)
</script>

<style scoped lang="scss">
.burger-menu-container {
  display: block;
  position: relative;

  @media (min-width: $mobile) {
    display: none;
  }
}

.burger-menu {
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 4px;
  width: 20px;
  height: 20px;
  cursor: pointer;

  &__line {
    width: 100%;
    height: 1.5px;
    background-color: black;
    transition: transform $animation-speed;
  }

  &--open {
    .burger-menu__line:first-child {
      transform: rotate(45deg) translate(2px, 2px);
    }

    .burger-menu__line:last-child {
      transform: rotate(-45deg) translate(2px, -2px);
    }
  }
}

.navigation {
  position: absolute;
  right: -10px;
  top: 100%;
  overflow: hidden;
  z-index: 10;
  padding: 5px 10px;
}
</style>
