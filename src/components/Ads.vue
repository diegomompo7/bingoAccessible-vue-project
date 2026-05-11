<script setup lang="ts">

import { nextTick, ref, watch } from 'vue';
import Banner from './Banner.vue';

const props = defineProps<{
    adsButton: boolean;
}>();

const adsUrl = import.meta.glob('@/assets/ads/*.mp4', {
    eager: true,
    query: '?url',
    import: 'default',
})

const ads: string[] = Object.values(adsUrl) as string[]

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
            class="video-ad w-1_1 "
            ref="videoRef"
            :src="ads[currentIndex]" 
            autoplay
            @ended="onEnded"
        />
        <Banner :ad="`ad${currentIndex+1}`" class="fixed-bottom  p-3_5 text-center"></Banner>
    </div>
</template>

<style scoped>
.video-ad {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    max-width: 80vh;   /* que no tape el banner de abajo */
    object-fit: contain;
}
</style>
