<template>
  <q-page class="column justify-center items-center">
    <Vue3Lottie :animationData="error" :height="200" :width="200" />
    <div class="nunito text-h4">Página em desenvolvimento</div>
  </q-page>
</template>

<script setup lang="ts">
import { Vue3Lottie } from 'vue3-lottie';
import error from '../assets/lottie/error.json';
</script>
