<template>
  <div class="dropdown" ref="root">
    <!-- Левый список -->
    <aside class="dropdown__left">
      <button
        v-for="(item, i) in props.items"
        :key="i"
        class="dropdown__item"
        :class="{ 'dropdown__item--active': i === active }"
        @mouseenter="active = i"
      >
        <div class="dropdown__left__title">
          <component :is="item.icon" class="dropdown__icon" />
          {{ item.title }}
        </div>
        <svgo-right-arrow v-if="item.arrow" class="dropdown__arrow" />
      </button>
    </aside>

    <!-- Правые столбцы -->
    <section class="dropdown__right" v-if="current">
      <div class="dropdown__column">
        <h3>{{ current.titleMain }}</h3>
        <ul>
          <li v-for="c in current.children1" :key="c.title">
            <nuxt-link to="#">
              {{ c.title }} <span>{{ c.count }}</span>
              <svgo-right-arrow v-if="c.arrow" class="dropdown__arrow__right" />
            </nuxt-link>
          </li>
        </ul>
      </div>

      <div class="dropdown__column">
        <h3>{{ current.titleSecondary }}</h3>
        <ul>
          <li v-for="c in current.children2" :key="c.title">
            <nuxt-link to="#">
              {{ c.title }} <span>{{ c.count }}</span>
            </nuxt-link>
          </li>
        </ul>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref, computed, onMounted, onBeforeUnmount } from 'vue'

/** Тип одного пункта меню */
export type ItemType = {
  title: string
  icon: string
  arrow?: boolean
  titleMain?: string
  titleSecondary?: string
  children1?: { title: string; count: number; arrow?: boolean }[]
  children2?: { title: string; count: number }[]
}

const props = defineProps<{
  /** Список пунктов меню */
  items: ItemType[]
  /** Кнопка-бургер, чтобы не закрывать меню при клике по ней */
  ignoreElement?: HTMLElement | null
  /** Какой пункт активен при открытии */
  defaultActive?: number
}>()

const emit = defineEmits(['close'])

/* ——— реактивность ——— */
const active  = ref(props.defaultActive ?? 0)
const current = computed(() => props.items[active.value])

/* ——— закрытие по Escape и клику вне ——— */
const root = ref<HTMLElement | null>(null)

function onClick(e: MouseEvent) {
  const inside = root.value?.contains(e.target as Node)
  const onBurger = props.ignoreElement?.contains?.(e.target as Node)
  if (!inside && !onBurger) emit('close')
}
function onKey(e: KeyboardEvent) {
  if (e.key === 'Escape') emit('close')
}

onMounted(() => {
  window.addEventListener('keydown', onKey)
  document.addEventListener('click', onClick, true)
})
onBeforeUnmount(() => {
  window.removeEventListener('keydown', onKey)
  document.removeEventListener('click', onClick, true)
})
</script>
