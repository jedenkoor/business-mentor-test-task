<template>
  <section class="tariffs">
    <BaseContainer>
      <p class="tariffs__text">Выберите лучший</p>
      <h1 class="tariffs__title">Актуальные тарифы</h1>
      <ul class="tariffs__list">
        <li
          v-for="(tariff, type) in tariffs"
          :key="type"
          :class="['tariffs__item', { 'tariffs__item--best': tariff.best }, { 'tariffs__item--timer': tariff.timer }]"
        >
          <BlocksTariff :type :tariff/>
        </li>
      </ul>
    </BaseContainer>
  </section>
</template>

<script setup lang="ts">
import BaseContainer from "~/components/Wraps/Container/BaseContainer.vue";
import BaseIcon from "~/components/Ui/Icon/BaseIcon.vue";

const tariffs = {
  consult: {
    title: 'Консультация',
    subtitle: 'Основные вопросы и направления',
    price: 'Бесплатно',
    subprice: 'В любое время',
    advantages: [
      'В любое удобное время',
      'Расскажем о всех нюансах процедуры',
      'Предложим варианты решения вашей проблемы',
      'Подготовим рекомендаци'
    ],
    guarantee: false,
    best: false,
    timer: null
  },
  base: {
    title: 'Базовый тариф',
    subtitle: 'От любого банка без процентов и переплат',
    price: '65 000 ₽',
    subprice: 'Единоразовый платеж',
    advantages: [
      'Сбор всех необходимых документов',
      'Сбор всех необходимых документов',
      'Взаимодействие с финансовым управляющим',
      'Контроль процедуры реализац. имущества',
      'Поддержка и сопровождение клиента на всех этапах банкротства'
    ],
    guarantee: true,
    best: true,
    timer: null
  },
  installments: {
    title: 'Рассрочка',
    subtitle: 'От любого банка без процентов и переплат',
    price: '3880 ₽ / мес.',
    subprice: 'На 24 месяца',
    advantages: [
      'Удобные варианты рассрочки',
      'Комфортные условия оплаты',
      'Фиксированная сумма',
      'Гарантия возврата средств',
      'Остальное, что и в базовом тарифе'
    ],
    guarantee: true,
    best: false,
    // timer: 4000,
    // timer: 3605000,
    timer: 81370000 // '22:36:10' в миллисекундах
  }
}
</script>

<style lang="scss">
@import "index-tariffs";
</style>