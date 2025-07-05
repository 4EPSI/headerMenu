<template>
  <div class="dropdown" ref="root">
    <!-- Левый список -->
    <aside class="dropdown__left">
      <button
        v-for="(item, i) in items"
        :key="i"
        class="dropdown__item"
        @mouseenter="active = i"
      >
        <div class="dropdown__left__title">
          <svgo-phone-rudjosz />
          {{ item.title }}
        </div>
        <svgo-right-arrow />
      </button>
    </aside>

    <!-- Правые столбцы -->
    <section class="dropdown__right" v-if="current">
      <div class="dropdown__column">
        <h3>{{ current.titleMain }}</h3>
        <ul>
          <li v-for="c in current.children1" :key="c.title">
            {{ c.title }} <span>{{ c.count }}</span>
          </li>
        </ul>
      </div>

      <div class="dropdown__column">
        <h3>{{ current.titleSecondary }}</h3>
        <ul>
          <li v-for="c in current.children2" :key="c.title">
            {{ c.title }} <span>{{ c.count }}</span>
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
    titleMain: 'Смартфоны',
    children1: [
      { title: 'Apple iPhone', count: 123 },
      { title: 'Смартфоны',    count: 227 },
      { title: 'iPhone 16',    count: 120 }
    ],
    titleSecondary: 'Гаджеты',
    children2: [
      { title: 'Смарт-часы',   count: 15 },
      { title: 'Смарт-кольца', count: 34 }
    ]
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
