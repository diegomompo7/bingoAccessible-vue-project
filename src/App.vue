<script setup lang="ts">
import { ref } from 'vue';
import Ads from './components/Ads.vue';
import Bingo from './components/Bingo.vue';

const adsActive = ref(false);
const currentNumber = ref('');
</script>

<template>
  <header class="controls" role="banner">
    <div class="controls__inner">
      <label class="controls__label" for="bingo-number">Número</label>
      <input
        id="bingo-number"
        class="controls__input"
        type="number"
        min="1"
        max="90"
        inputmode="numeric"
        autocomplete="off"
        v-model="currentNumber"
        aria-label="Introduce el número de bingo"
      />
      <button
        class="controls__btn controls__btn--ad"
        @click="adsActive = true"
        :aria-pressed="adsActive"
      >
        Anuncio
      </button>
      <button
        class="controls__btn controls__btn--bingo"
        @click="adsActive = false"
        :aria-pressed="!adsActive"
      >
        Bingo
      </button>
    </div>
  </header>

  <main role="main">
    <Bingo :number="currentNumber" :adsActive="adsActive" />
    <Ads :adsActive="adsActive" />
  </main>
</template>

<style lang="scss" scoped>
.controls {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: var(--z-overlay);
  background: rgba(0, 0, 0, 0.88);
  backdrop-filter: blur(6px);
  padding: var(--space-xs) var(--space-md);

  &__inner {
    display: flex;
    align-items: center;
    gap: var(--space-sm);
  }

  &__label {
    color: var(--color-text-muted);
    font-weight: var(--font-weight-semibold);
    font-size: var(--text-sm);
    white-space: nowrap;
  }

  &__input {
    width: 5rem;
    padding: 0.3rem 0.5rem;
    font-family: 'Atkinson Hyperlegible', sans-serif;
    font-size: var(--text-lg);
    font-weight: var(--font-weight-bold);
    text-align: center;
    background: var(--color-surface);
    color: var(--color-accent);
    border: 2px solid var(--color-accent);
    border-radius: var(--radius-sm);
    min-height: var(--touch-min);

    &:focus-visible {
      outline: 3px solid var(--color-accent);
      outline-offset: 2px;
    }

    // Remove browser number spin buttons — not useful here
    &::-webkit-inner-spin-button,
    &::-webkit-outer-spin-button { appearance: none; }
  }

  &__btn {
    min-height: var(--touch-min);
    padding: 0 var(--space-md);
    font-family: 'Atkinson Hyperlegible', sans-serif;
    font-weight: var(--font-weight-bold);
    font-size: var(--text-sm);
    border: 2px solid transparent;
    border-radius: var(--radius-sm);
    cursor: pointer;
    transition: box-shadow var(--transition-fast);

    &:focus-visible {
      outline: 3px solid var(--color-accent);
      outline-offset: 2px;
    }

    &--ad {
      background: var(--color-accent);
      color: #000;

      &[aria-pressed="true"] {
        box-shadow: var(--glow-md);
      }
    }

    &--bingo {
      background: transparent;
      color: var(--color-accent);
      border-color: var(--color-accent);

      &[aria-pressed="true"] {
        box-shadow: var(--glow-sm);
      }
    }
  }
}
</style>
