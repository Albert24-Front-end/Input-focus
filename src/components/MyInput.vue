<script setup lang="ts">
import { useTemplateRef } from 'vue';

const input = useTemplateRef('input')
defineExpose({
  focus() {
    input.value?.focus()
  }
})
</script>

<template>
  <input ref="input" type="text" />
  <div class="error"></div>
</template>
