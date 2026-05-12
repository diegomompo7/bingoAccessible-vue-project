<script setup lang="ts">
import { nextTick, ref, watch } from 'vue';
import Banner from './Banner.vue';

const props = defineProps<{
  adsActive: boolean;
}>();

const adsUrlVideo = import.meta.glob('@/assets/ads/*.mp4', {
  eager: true,
  query: '?url',
  import: 'default',
});

const adsUrlImage = import.meta.glob('@/assets/ads/*.jpg', {
  eager: true,
  query: '?url',
  import: 'default',
});

const imageUrls = Object.values(adsUrlImage) as string[];
const ads = Object.values(adsUrlVideo).map((video, i) => ({
  video: video as string,
  image: (imageUrls[i] ?? '') as string,
}));

const currentIndex = ref(0);
const started = ref(false);
const videoRef = ref<HTMLVideoElement | null>(null);

watch(() => props.adsActive, async (isOn) => {
  if (!ads.length) return;
  if (isOn) {
    if (started.value) {
      currentIndex.value = (currentIndex.value + 1) % ads.length;
    }
    started.value = true;
    await nextTick();
    videoRef.value?.load();
    videoRef.value?.play();
  } else {
    videoRef.value?.pause();
  }
});

const onEnded = () => {
  currentIndex.value = (currentIndex.value + 1) % ads.length;
  nextTick(() => {
    videoRef.value?.load();
    videoRef.value?.play();
  });
};
</script>

<template>
  <div
    v-show="props.adsActive"
    class="ads-wrapper"
    role="region"
    aria-label="Anuncio de patrocinador"
  >
    <video
      class="ad-media ad-media--video"
      ref="videoRef"
      :src="ads[currentIndex]?.video"
      :aria-label="`Anuncio ${currentIndex + 1}`"
      playsinline
      @ended="onEnded"
    />
    <img
      :src="ads[currentIndex]?.image"
      :alt="`Anuncio ${currentIndex + 1} de la Foguera Sant Blai de Dalt`"
      class="ad-media ad-media--image"
    />
    <Banner
      :ad="`ad${currentIndex + 1}`"
      class="ad-banner"
    />
  </div>
</template>

<style lang="scss" scoped>
@import "../scss/bootstrap-mixins";

.ads-wrapper {
  position: fixed;
  inset: 0;
  background: var(--color-bg);
}

.ad-media {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  object-fit: contain;
  max-width: 100%;
  max-height: 100%;
}

.ad-banner {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
}

@include media-breakpoint-up(sm) {
  .ad-media--image { display: none; }
  .ad-banner        { display: none; }
}

@include media-breakpoint-down(sm) {
  .ad-media--video  { display: none; }
  .ad-media--image  { max-width: 95vw; }
}
</style>
