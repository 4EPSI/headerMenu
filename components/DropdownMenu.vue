<template>
  <div class="dropdown" ref="root">
    <!-- Левый список -->
    <aside class="dropdown__left">
      <button
        v-for="(item, i) in items"
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
              <svgo-right-arrow 
              v-if="c.arrow" 
              class="dropdown__arrow__right" 
            />
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

const props = defineProps<{
  ignoreElement?: HTMLElement | null
}>()

/* ——— данные меню ——— */
const items = [
  {
    title: 'Смартфоны и гаджеты',
    icon: 'svgo-phone-rudjosz',
    arrow: true,
    titleMain: 'Смартфоны',
    children1: [
      { title: 'Apple iPhone', count: 123, arrow: false },
      { title: 'Смартфоны',    count: 227, arrow: true },
      { title: 'iPhone 16',    count: 120, arrow: false },
      { title: 'Складные',    count: 30, arrow: false },
      { title: 'realme',    count: 120, arrow: false },
      { title: 'Huawei Mate X6',    count: 100, arrow: false },
      { title: 'Кнопочные',    count: 23, arrow: false },
      { title: 'Домашние',    count: 17, arrow: false },
      { title: 'Samsung',    count: 27, arrow: false }
    ],
    titleSecondary: 'Гаджеты',
    children2: [
      { title: 'Смарт-часы',   count: 15 },
      { title: 'Смарт-кольца', count: 34 },
      { title: 'Наушники', count: 21 },
      { title: 'Гарнитуры', count: 12 },
      { title: 'Портативное аудио', count: 42 },
      { title: 'Умные гаджеты', count: 46 },
      { title: 'Очки VR', count: 49 },
      { title: 'Для блогеров', count: 32 },
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
  // …добавь остальные пункты
]

/* ——— реактивность ——— */
const active  = ref(0)
const current = computed(() => items[active.value])

/* ——— закрытие меню ——— */
const emit = defineEmits(['close'])
const root = ref<HTMLElement | null>(null)

function onClick(e: MouseEvent) {
  const clickedInside = root.value?.contains(e.target as Node)
  const clickedBurger = props.ignoreElement?.contains?.(e.target as Node)
  if (!clickedInside && !clickedBurger) {
    emit('close')
  }
}
function onKey(e: KeyboardEvent) {
  if (e.key === 'Escape') emit('close')
}

onMounted(() => {
  window.addEventListener('keydown', onKey)
  document.addEventListener('click', onClick, true)   // capture = true
})
onBeforeUnmount(() => {
  window.removeEventListener('keydown', onKey)
  document.removeEventListener('click', onClick, true)
})
</script>
