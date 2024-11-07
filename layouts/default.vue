<template>
  <BaseWrapper>
    <BaseContent>
      <slot />
    </BaseContent>
  </BaseWrapper>
</template>

<script setup lang="ts">
import BaseWrapper from '~/components/Wraps/Wrapper/BaseWrapper.vue'
import BaseContent from '~/components/Wraps/Content/BaseContent.vue'
</script>
