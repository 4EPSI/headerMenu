<template>
  <div class="header-main">
    <!-- Логотип -->
    <nuxt-link to="/"><img :src="logoSrc" alt="logo" /></nuxt-link>

    <!-- Правая часть -->
    <div class="header-right">
      <div class="header-content">
        <!-- Бургер -->
        <button
          ref="burgerBtn"
          class="burger-menu"
          :class="{ active: isActive }"
          @click="toggle"
          aria-label="Toggle menu"
        >
          <span class="burger-line"></span>
          <span class="burger-line"></span>
          <span class="burger-line"></span>
        </button>

        <!-- Dropdown -->
        <DropdownMenu
          v-if="isActive"
          :items="menuItems"
          :ignore-element="burgerBtn"
          :default-active="0"
          @close="isActive = false"
        />

        <!-- Поиск -->
        <div class="search-container">
          <input
            v-model="query"
            type="text"
            class="search-input"
            placeholder="Поиск товаров..."
          />
          <button class="search-btn">Найти</button>
        </div>

        <!-- Контакты -->
        <div class="header-contacts">
          <nuxt-link to="#"><svgo-telegram /></nuxt-link>
          <nuxt-link to="#"><svgo-whatsapp /></nuxt-link>
        </div>
      </div>

      <!-- Линия ссылок -->
      <HeaderNavLink />


    </div>

    <!-- Селектор языка -->
    <div class="lang-switcher">
      <span class="globe"><svgo-planet /></span>
      <span
        :class="['lang', current === 'ru' && 'active']"
        @click="setLang('ru')"
      >RU</span>
      <span class="divider">|</span>
      <span
        :class="['lang', current === 'en' && 'active']"
        @click="setLang('en')"
      >EN</span>
    </div>

    <!-- Иконки + «Собрать ПК» -->
    <div>
      <div class="header-icons">
        <button><svgo-like /></button>
        <button><svgo-hunter /></button>
        <button><svgo-chest /></button>
      </div>
      <HeaderNavButtonPlus />
    </div>
  </div>
</template>

<script setup lang="ts">
// import { ref, watch } from 'vue'
// import DropdownMenu, { ItemType } from '@/components/DropdownMenu.vue'

/* ——— состояния ——— */
const logoSrc  = '/img/logo.svg'
const query    = ref('')
const isActive = ref(false)
const burgerBtn = ref<HTMLElement | null>(null)

/* ——— данные меню (можно вынести в отдельный файл) ——— */
const menuItems: ItemType[] = [
  {
    title: 'Смартфоны и гаджеты',
    icon: 'svgo-phone-rudjosz',
    arrow: true,
    titleMain: 'Смартфоны',
    children1: [
      { title: 'Apple iPhone', count: 123, arrow: false },
      { title: 'Смартфоны',    count: 227, arrow: true },
      { title: 'iPhone 16',    count: 120, arrow: false },
      { title: 'Складные',     count: 30,  arrow: false },
      { title: 'realme',       count: 120, arrow: false },
      { title: 'Huawei Mate X6', count: 100, arrow: false },
      { title: 'Кнопочные',    count: 23,  arrow: false },
      { title: 'Домашние',     count: 17,  arrow: false },
      { title: 'Samsung',      count: 27,  arrow: false }
    ],
    titleSecondary: 'Гаджеты',
    children2: [
      { title: 'Смарт-часы',        count: 15 },
      { title: 'Смарт-кольца',      count: 34 },
      { title: 'Наушники',          count: 21 },
      { title: 'Гарнитуры',         count: 12 },
      { title: 'Портативное аудио', count: 42 },
      { title: 'Умные гаджеты',     count: 46 },
      { title: 'Очки VR',           count: 49 },
      { title: 'Для блогеров',      count: 32 }
    ]
  },
  {
    title: 'Ноутбуки и компьютеры',
    icon: 'svgo-laptop',
    arrow: true
  },
  {
    title: 'Телевизоры и цифровое ТВ',
    icon: 'svgo-tv',
    arrow: true
  },
  {
    title: 'Аудиотехника',
    icon: 'svgo-audio',
    arrow: true
  },
  {
    title: 'Акции',
    icon: 'svgo-stock-bg',
    arrow: false
  },
  {
    title: 'Новинки',
    icon: 'svgo-new',
    arrow: false
  }
]

/* ——— методы ——— */
function toggle() { isActive.value = !isActive.value }

/* ——— эмит наверх, если нужно ——— */
const emit = defineEmits(['toggle'])
watch(isActive, v => emit('toggle', v))

/* ——— смена языка ——— */
const current = ref<'ru' | 'en'>('ru')
function setLang(lang: 'ru' | 'en') { current.value = lang }
</script>

<style scoped lang="scss">
/* твои стили header-компонента */
</style>