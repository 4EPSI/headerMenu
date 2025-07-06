<template>
  <div class="nav-links">
    <nuxt-link
      v-for="(item, i) in navItems"
      :key="i"
      to="#"
      class="nav-links__item"
    >
      <component :is="item.icon" />
      {{ item.title }}
    </nuxt-link>
  </div>
</template>

<script setup lang="ts">
const navItems = [
  { title: 'Акции', icon: 'svgo-stock' },
  { title: 'Горячее предложение', icon: 'svgo-lightning' },
  { title: 'Подарочные наборы', icon: 'svgo-gift' },
  { title: 'События', icon: 'svgo-quest' },
  { title: 'Наши бренды', icon: 'svgo-orc' }
]
</script>

<style lang="scss" scoped>
@use '@/assets/scss/blocks/nav-links' as *;
</style>