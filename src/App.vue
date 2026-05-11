<script setup lang="ts">
import { ref } from 'vue';
import Ads from './components/Ads.vue';
import Bingo from './components/Bingo.vue';

const adsButton = ref(false);
</script>

<template>
  <button class="btn-ad" @click="adsButton=true" >Start</button>
  <button class="btn-ad" @click="adsButton=false">Stop</button>
  <Bingo :adsButton="adsButton"></Bingo>
  <Ads :adsButton="adsButton"/>
</template>

<style scoped>

</style>
