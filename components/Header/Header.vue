<template>
  <header class="header">
    <HeaderTop />
    <HeaderMain />
    <!-- <div class="header__container">
      <NuxtLink to="/" class="header__logo">Test</NuxtLink>

      <nav :class="['header__nav', { 'header__nav--open': isMenuOpen }]">
        <ul class="nav__list">
          <li class="nav__item"><a href="#" class="nav__link">Главная</a></li>
          <li class="nav__item"><a href="#" class="nav__link">О нас</a></li>
          <li class="nav__item"><a href="#" class="nav__link">Контакты</a></li>
        </ul>
        <button class="header__login">Войти</button>
      </nav>

      <button
        class="header__burger"
        @click="toggleMenu"
        aria-label="Открыть меню"
        :aria-expanded="isMenuOpen"
      >
        <span class="burger__line" />
        <span class="burger__line" />
        <span class="burger__line" />
      </button>
    </div> -->
  </header>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const isMenuOpen = ref(false)

function toggleMenu() {
  isMenuOpen.value = !isMenuOpen.value
}
</script>