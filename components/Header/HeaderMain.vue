<template>
  <div class="header-main">
    <div>
      <nuxt-link to="/">
        <img :src="logoSrc" alt="logo" />
      </nuxt-link>
    </div>
    <div class="header-search">
      <button 
        class="burger-menu" 
        :class="{ 'active': isActive }"
        @click="toggle"
        aria-label="Toggle menu"
      >
        <span class="burger-line"></span>
        <span class="burger-line"></span>
        <span class="burger-line"></span>
      </button>

      <div class="search-container">
        <input
          type="text"
          class="search-input"
          placeholder="Поиск товаров..."
          v-model="query"
        />
        <button class="search-btn">Найти</button>
      </div>

      <div class="header-contacts">
        <nuxt-link to="#">
          <svgo-telegram />
        </nuxt-link>

        <nuxt-link to="#">
          <svgo-whatsapp />
        </nuxt-link>
      </div>
    </div>

    <div class="lang-switcher">
      <span class="globe">
        <svgo-planet />
      </span>
      <div class="lang-container">
        <span
          :class="['lang', current === 'ru' ? 'active' : '']"
          @click="setLang('ru')"
        >RU</span>
        <span class="divider">|</span>
        <span
          :class="['lang', current === 'en' ? 'active' : '']"
          @click="setLang('en')"
        >EN</span>

      </div>
    </div>
    <div class="header-icons">
      <button>
        <svgo-like />
      </button>
      <button>
        <svgo-hunter />
      </button>
      <button>
        <svgo-chest />
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const query = ref('')
const logoSrc = '/img/logo.svg'
const isActive = ref(false)

const toggle = () => {
  isActive.value = !isActive.value
}

// Эмит для родительского компонента
const emit = defineEmits(['toggle'])

watch(isActive, (newValue) => {
  emit('toggle', newValue)
})



const current = ref('ru')
const setLang = (lang) => {
  current.value = lang
  // Здесь можно добавить логику смены языка приложения
}
</script>