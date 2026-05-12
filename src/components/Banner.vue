<script setup lang="ts">
defineProps<{
  ad: string | undefined;
}>();
</script>

<template>
  <div :class="`bg-${ad}`" class="banner" role="complementary" aria-label="Información del patrocinador">
    <p class="banner__text">Más información</p>
  </div>
</template>

<style scoped>
.banner {
  padding: 1rem 1.5rem;
}

.banner__text {
  margin: 0;
  color: #fff;
  font-family: 'Atkinson Hyperlegible', sans-serif;
  font-weight: 700;
  font-size: clamp(1rem, 3vw, 1.5rem);
}
</style>
