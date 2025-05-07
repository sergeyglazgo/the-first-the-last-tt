<template>
  <button
    class="language-selector"
    @mouseenter="showLanguages"
    @mouseleave="hideLanguages"
    @click="toggleDropdown"
  >
    <div class="language-selector__icon">
      <span>&#128069;</span>
    </div>
    <div
      v-show="isShowingLanguages"
      class="language-selector__options"
      :class="{ 'language-selector__options--show': isShowingLanguages }"
    >
      <div
        v-for="(lang, index) in availableLanguages"
        :key="lang"
        class="language-selector__option"
        :class="{ 'language-selector__option--selected': lang === currentLanguage }"
        :style="{ animationDelay: `${index * 0.1}s` }"
        @click.stop="selectLanguage(lang)"
      >
        {{ lang }}
      </div>
    </div>
  </button>
</template>

<script setup>
import { ref } from 'vue'

const currentLanguage = ref('eng')
const availableLanguages = ref(['eng', 'ua'])
const isShowingLanguages = ref(false)

const selectLanguage = (lang) => {
  currentLanguage.value = lang
  hideLanguages()
}

const showLanguages = () => {
  isShowingLanguages.value = true
}

const hideLanguages = () => {
  isShowingLanguages.value = false
}

const toggleDropdown = () => {
  isShowingLanguages.value = !isShowingLanguages.value
}
</script>

<style scoped lang="scss">
.language-selector {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  width: 34px;
  height: 34px;
  background-color: transparent;
  font-size: inherit;
  font-family: 'GrtskGiga', sans-serif;
  border: rgba(255, 255, 255, 0.5) solid 1px;
  border-radius: 50%;

  &__icon {
    width: 14px;
    height: 20px;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  &__options {
    position: absolute;
    left: -10px;
    top: 100%;
    overflow: hidden;
    z-index: 10;
    padding: 5px;

    &--show .language-selector__option {
      animation: slideIn $animation-speed forwards;
    }
  }

  &__option {
    padding: 3px 6px;
    cursor: pointer;
    opacity: 0;
    transition: color $animation-speed ease;
    transform: translateX(-20px);
    text-align: start;

    &:hover {
      color: white;
    }

    &:not(.language-selector__option--selected):hover::after {
      width: 100%;
    }

    &::after {
      content: '';
      position: absolute;
      bottom: 0;
      left: 0;
      width: 0;
      height: 2px;
      background-color: white;
      transition: width $animation-speed ease;
    }

    &--selected {
      color: white;
      cursor: default;
    }
  }
}

@media (min-width: $tablet) {
  .language-selector {
    width: 38px;
    height: 38px;

    &__icon {
      width: 15px;
      height: 21px;
    }

    &__option {
      padding: 5px 0;
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
