<template>
  <component v-if="iconComponent" :is="iconComponent" :fill="fill" />
</template>

<script setup lang="ts">
import { shallowRef, watch } from 'vue'

const props = defineProps({
  icon: {
    type: String,
    required: true
  },
  fill: {
    type: String,
    default: 'unset'
  }
})

// Загрузка всех SVG-иконок
const icons = Object.fromEntries(
  Object.entries(import.meta.glob('~/assets/icons/**/*.svg', { eager: true })).map(
    ([key, value]) => {
      const filename = key.split('/').pop()!.split('.').shift()
      return [filename, value]
    }
  )
)

const iconComponent = shallowRef()

// Загрузка иконки при изменении пропса
watch(() => props.icon, () => {
  iconComponent.value = icons?.[props.icon]?.default || null
}, { immediate: true })
</script>

<style scoped lang="scss">
@import "base-icon";
</style>
