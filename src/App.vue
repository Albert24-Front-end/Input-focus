<script setup lang="ts">
import { useIdUpload } from './composables/useIdUpload';

const { isLoading, isIdProvided, isExtraSpellingNeeded, upload } = useIdUpload();

const vFocus = {
  mounted(el: HTMLInputElement) {
    el.focus()
  }
}

</script>

<template>
  <h1>Identification Form</h1>
  <button :disabled="isLoading" @click="upload">
    <template v-if="!isLoading">Provide ID</template>
    <template v-else>Loading</template>
  </button>
  <p v-if="isIdProvided">
    <label>Provide your name in English</label><span v-if="isExtraSpellingNeeded" class="required">(required)</span>:
    <input v-focus/>
  </p>
</template>

<style>
.required{
  color: red;
}
</style>
