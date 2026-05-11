<script setup lang="ts">
import { ref } from 'vue';
import Ads from './components/Ads.vue';

const adsButton = ref(false);
</script>

<template>
  <button @click="adsButton=true" >Start</button>
  <button @click="adsButton=false">Stop</button>
  <Ads :adsButton="adsButton"/>
</template>

<style scoped></style>
