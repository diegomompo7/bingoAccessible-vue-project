<script setup lang="ts">

import { nextTick, ref, watch } from 'vue';
import Banner from './Banner.vue';

const props = defineProps<{
    adsButton: boolean;
}>();

const adsUrlVideo = import.meta.glob('@/assets/ads/*.mp4', {
    eager: true,
    query: '?url',
    import: 'default',
})

const adsUrlImage = import.meta.glob('@/assets/ads/*.jpg', {
    eager: true,
    query: '?url',
    import: 'default',
})

const imageUrls = Object.values(adsUrlImage) as string[]
const ads = Object.values(adsUrlVideo).map((video, i) => ({
    video: video as string,
    image: (imageUrls[i] ?? '') as string,
}))

const currentIndex = ref(0)
const started = ref(false)
const videoRef = ref<HTMLVideoElement | null>(null)

watch(() => props.adsButton, async (isOn) => {
    if(!ads.length) return
    if (isOn) {
        if(started.value){
            currentIndex.value = (currentIndex.value + 1) % ads.length
        }
        started.value = true
        await nextTick()
        videoRef.value?.load()
        videoRef.value?.play()
    } else {
        videoRef.value?.pause()
    }
})

const onEnded = () => {
  currentIndex.value = (currentIndex.value + 1) % ads.length
  nextTick(() => {
    videoRef.value?.load()
    videoRef.value?.play()
  })
}



</script>

<template>
    <div v-show="props.adsButton" class="">
        <video
            class="video-ad w-1_1"
            ref="videoRef"
            :src="ads[currentIndex]?.video"
            autoplay
            @ended="onEnded"
        />
        <b-container fluid="sm">
            <img :src="ads[currentIndex]?.image" alt="" class="image-ad w-1_1" fluid="sm">
            <Banner :ad="`ad${currentIndex+1}`" class="banner-ad fixed-bottom  p-4_5 text-center"></Banner>
        </b-container>
    </div>
</template>

<style lang="scss" scoped>
@import "../scss/bootstrap-mixins";

.video-ad,
.image-ad {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    object-fit: contain;
}
 @include media-breakpoint-up(sm)  { .image-ad{display: none;} .banner-ad{display: none;}}
 @include media-breakpoint-down(sm)  { .video-ad{display: none;} .image-ad{max-width: 95vw;}}

</style>
