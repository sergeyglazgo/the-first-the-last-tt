<template>
  <nav class="navigation">
    <ul class="navigation__list">
      <li
        v-for="(item, index) in navItems"
        :key="index"
        class="navigation__item"
        :style="{ animationDelay: `${index * 0.1}s` }"
        @click="closeMenu"
      >
        <router-link :to="item.path" class="navigation__link">
          <span>{{ item.name }}</span>
        </router-link>
      </li>
    </ul>
  </nav>
</template>

<script setup>
const emit = defineEmits(['close'])

const navItems = [
  { name: 'who?', path: '/details' },
  { name: 'where?', path: '/details' },
  { name: 'what?', path: '/details' }
]

const closeMenu = () => {
  emit('close')
}
</script>

<style scoped lang="scss">
.navigation {
  &__list {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: flex-end;
    list-style: none;
    padding: 5px;
    margin: 0;
  }

  &__item {
    opacity: 0;
    transform: translateX(20px);
    animation: slideIn 0.3s forwards;
  }

  &__link {
    text-decoration: none;
    color: black;
    transition: color 0.3s ease;
    position: relative;
    display: inline-block;
    padding: 5px 0;

    &:hover {
      color: white;

      &::after {
        width: 100%;
      }
    }

    &::after {
      content: '';
      position: absolute;
      bottom: 0;
      left: 0;
      width: 0;
      height: 2px;
      background-color: white;
      transition: width 0.3s ease;
    }
  }
}

@media (min-width: $mobile) {
  .navigation {
    &__list {
      padding: 0;
      flex-direction: unset;
    }

    &__link {
      padding: 0;
    }

    &__item {
      position: absolute;
      opacity: 1;
      transform: none;
      animation: none;

      &:nth-child(1) {
        left: 50%;
        transform: translateX(-50%);
        bottom: 12px;
      }

      &:nth-child(2) {
        left: -24px;
        top: 50%;
        transform: translateY(-50%) rotate(-90deg);
      }

      &:nth-child(3) {
        right: -18px;
        top: 50%;
        transform: translateY(-50%) rotate(90deg);
      }
    }
  }
}

@keyframes slideIn {
  to {
    opacity: 1;
    transform: translateX(0);
  }
}
</style>
