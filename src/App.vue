<script setup lang="ts">
import { useTemplateRef, watch } from 'vue';
import { useIdUpload, } from './composables/useIdUpload';

const { isLoading, isIdProvided, isExtraSpellingNeeded, upload } = useIdUpload();

const input = useTemplateRef('extraName')

watch(input, () => {
  if (isExtraSpellingNeeded.value){
    input.value?.focus()
  }
})

</script>

<template>
  <h1>Identification Form</h1>
  <button :disabled="isLoading" @click="upload">
    <template v-if="!isLoading">Provide ID</template>
    <template v-else>Loading</template>
  </button>
  <p v-if="isIdProvided">
    <label>Provide your name in English</label><span v-if="isExtraSpellingNeeded" class="required">(required)</span>:
    <input ref="extraName"/>
  </p>
</template>

<style>
.required{
  color: red;
}
</style>
