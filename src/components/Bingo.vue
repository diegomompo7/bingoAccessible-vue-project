<script setup lang="ts">
defineProps<{
  number: string;
  adsActive: boolean;
}>();
</script>

<template>
  <div
    v-show="!adsActive"
    class="bingo-display"
    role="status"
    aria-live="assertive"
    aria-label="Número de bingo"
  >
    <span class="bingo-display__number">
      {{ number || '—' }}
    </span>
  </div>
</template>

<style lang="scss" scoped>
.bingo-display {
  position: fixed;
  inset: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  background: var(--color-bg);

  &__number {
    font-size: min(80vw, 120vh);
    font-weight: var(--font-weight-bold);
    color: var(--color-accent);
    line-height: 1;
    text-shadow: var(--glow-lg);
    user-select: none;
  }
}
</style>
