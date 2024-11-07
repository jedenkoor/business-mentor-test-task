<template>
  <BaseWrapper>
    <BaseContent class="error">
      <BaseContainer class="error__container">
        <div class="error__title">
          {{ error.message.split(':')[0] }}
        </div>
        <NuxtLink class="error__btn" to="/">На главную</NuxtLink>
      </BaseContainer>
    </BaseContent>
  </BaseWrapper>
</template>

<script setup lang="ts">
import BaseWrapper from '~/components/Wraps/Wrapper/BaseWrapper.vue'
import BaseContent from '~/components/Wraps/Content/BaseContent.vue'
import BaseContainer from '~/components/Wraps/Container/BaseContainer.vue'

const props = defineProps({
  error: {
    type: Object,
    default: () => {}
  }
})

useHead({
  title: props.error.message.split(':')[0]
})

console.log(props.error)
</script>

<style scoped lang="scss">
.error {
  display: flex;
  align-items: center;
  justify-content: center;
  &__container {
    display: flex;
    align-items: center;
    flex-direction: column;
  }
  &__title {
    margin-bottom: 2rem;
    font-size: 3rem;
    text-align: center;
  }
  &__btn {
    padding: 1.4rem 4rem;
    border-radius: 0.6rem;
    background-color: var(--black-100);
    color: var(--white-100);
    font-weight: 600;
    line-height: 1.2;
    transition: background-color 0.2s;
    @include hover {
      &:hover {
        background-color: #595959;
      }
    }
    @include active {
      &:active {
        background-color: #595959;
      }
    }
  }
}
</style>