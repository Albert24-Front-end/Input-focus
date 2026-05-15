<script setup lang="ts">
import { useTemplateRef, watch } from 'vue';
import { useIdUpload, } from './composables/useIdUpload';
import MyInput from './components/MyInput.vue';

const { isLoading, isIdProvided, isExtraSpellingNeeded, upload } = useIdUpload();

const input = useTemplateRef('extraName')

 const focusIfNeeded = () => {
  if (isExtraSpellingNeeded.value){
    input.value?.focus()
  }
}

</script>

<template>
  <h1>Identification Form</h1>
  <button :disabled="isLoading" @click="upload">
    <template v-if="!isLoading">Provide ID</template>
    <template v-else>Loading</template>
  </button>
  <p v-if="isIdProvided && !isLoading">
    <label>Provide your name in English</label><span v-if="isExtraSpellingNeeded" class="required">(required)</span>:
    <MyInput @vue:mounted="focusIfNeeded" ref="extraName"/>
  </p>
</template>

<style>
.required{
  color: red;
}
</style>
