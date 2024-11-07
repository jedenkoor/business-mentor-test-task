<template>
  <div :class="['tariff', `tariff--${type}`, { 'tariff--best': tariff.best }]">
    <span v-if="tariff.best" class="tariff__best">Лучший тариф</span>
    <div class="tariff__wrap tariff__wrap--left">
      <div class="tariff__icon">
        <BaseIcon :icon="type" filled />
      </div>
      <h2 class="tariff__title">{{ tariff.title }}</h2>
      <p class="tariff__subtitle">{{ tariff.subtitle }}</p>
      <ul class="tariff__list tariff__list--tablet">
        <li v-for="(advantage, index) in tariff.advantages" :key="index" class="tariff-list__item">
          <BaseIcon icon="check" filled />
          <span>
          {{ advantage }}
          <img
            v-if="type ==='installments' && index === 0"
            class="tariff-list__variants"
            src="/tariff/variants.png"
            alt="Банки с рассрочкой"
          >
        </span>
        </li>
      </ul>
    </div>
    <div class="tariff__wrap">
      <div v-if="tariff.timer" class="tariff__timer" role="timer">
        <BaseIcon icon="clock" filled />
        <span>{{ restParsedTime }}</span>
      </div>
      <div class="tariff__block">
        <p class="tariff__price">{{ tariff.price }}</p>
        <p class="tariff__subprice">{{ tariff.subprice }}</p>
        <button class="tariff__btn" type="button" :disabled="tariff.timer && restTime < 1000" @click="handleClick(tariff.title)">
          Выбрать
        </button>
      </div>
      <div v-if="tariff.guarantee" class="tariff__guarantee">
        <span class="tariff__tooltip">
          <button class="tariff-tooltip__toggle" type="button" :aria-labelledby="`${type}-tooltip`">
            <BaseIcon icon="tooltip" filled />
          </button>
          <span class="tariff-tooltip__text" role="tooltip" :id="`${type}-tooltip`">Для Вашего спокойствия мы гарантируем возврат оплаты в случае отсутствия списания долгов после процедуры.</span>
        </span>
      </div>
    </div>
    <ul class="tariff__list">
      <li v-for="(advantage, index) in tariff.advantages" :key="index" class="tariff-list__item">
        <BaseIcon icon="check" filled />
        <span>
          {{ advantage }}
          <img
            v-if="type ==='installments' && index === 0"
            class="tariff-list__variants"
            src="/tariff/variants.png"
            alt="Банки с рассрочкой"
          >
        </span>
      </li>
    </ul>
  </div>
</template>

<script setup lang="ts">
import BaseIcon from "~/components/Ui/Icon/BaseIcon.vue";

const props = defineProps({
  type: {
    type: String,
    default: () => ''
  },
  tariff: {
    type: Object,
    default: () => {}
  }
})

onMounted(() => {
  if (props.tariff.timer) {
    initialTimer()
  }
})

const restParsedTime = computed(() => {
  const t = restTime.value
  let hours = Math.floor((t / (1000 * 60 * 60)) % 24)
  let minutes = Math.floor((t / (1000 * 60)) % 60)
  let seconds = Math.floor((t / 1000) % 60)
  hours = hours < 10 ? `0${hours}` : hours
  minutes = minutes < 10 ? `0${minutes}` : minutes
  seconds = seconds < 10 ? `0${seconds}` : seconds
  return `${hours}:${minutes}:${seconds}`
})

let restTime = ref(0)
let timer
const initialTimer = () => {
  clearInterval(timer)
  const endTimer = new Date().getTime() + props.tariff.timer
  restTime.value = endTimer - new Date().getTime()
  timer = setInterval(() => {
    if (endTimer < new Date().getTime()) {
      clearInterval(timer)
    } else {
      restTime.value = endTimer - new Date().getTime()
    }
  }, 1000)
}

const handleClick = (title) => {
  console.log(title)
}
</script>

<style lang="scss">
@import "blocks-tariff";
</style>