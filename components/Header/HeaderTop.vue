<template>
  <div class="header-top">
    <div class="header-top__icon">
      <nuxt-link to="https://www.google.com/maps/place/%D0%9B%D0%BE%D0%BD%D0%B4%D0%BE%D0%BD,+%D0%92%D0%B5%D0%BB%D0%B8%D0%BA%D0%BE%D0%B1%D1%80%D0%B8%D1%82%D0%B0%D0%BD%D0%B8%D1%8F/@51.5287398,-0.2664036,11z/data=!3m1!4b1!4m6!3m5!1s0x47d8a00baf21de75:0x52963a5addd52a99!8m2!3d51.5072178!4d-0.1275862!16zL20vMDRqcGw!5m1!1e1?entry=ttu&g_ep=EgoyMDI1MDYzMC4wIKXMDSoASAFQAw%3D%3D" target="_blank">
        <SvgoLocation />
        Сайлент-Хилл
      </nuxt-link>

      <nuxt-link to="tel:+7 555 555-37-50" class="header-top__icon">
        <SvgoPhone />
        +7 555 555-37-50
      </nuxt-link>
    </div>

    <div class="header-top__worktime">
      Ежедневно 9:00 – 21:00
    </div>

    <nav class="header-top__links">
      <nuxt-link to="#">Доставка</nuxt-link>
      <nuxt-link to="#">Оплата</nuxt-link>
      <nuxt-link to="#">Контакты</nuxt-link>
    </nav>
  </div>
</template>