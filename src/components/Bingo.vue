<script setup lang="ts">
const props = defineProps<{
    adsButton: boolean;
}>();
</script>

<template>
    <div v-show="!props.adsButton" class="position-fixed top-50 start-50 translate-middle text-center fs-text_12xl">
        <p>72</p>
    </div>
</template>

<style lang="scss" scoped>

div {
    font-size: 270px;
    //font-size: min(45vw, 80vh);
    @media (min-width: 320px) { font-size: min(80vw, 120vh);   }  // < 576px  (72px)

    //@include media-breakpoint-up(xs)  { font-size: 4.5rem;   }  // < 576px  (72px)
    //@include media-breakpoint-up(sm)  { font-size: 8rem;   }  // 576px  (128px)
    //@include media-breakpoint-up(md)  { font-size: 10.625rem; } // 768px (170px)
    //@include media-breakpoint-up(lg)  { font-size: 14.25rem; }  // 992px (228px)
    //@include media-breakpoint-up(xl)  { font-size: 19rem;  }   // 1200px (304px)
    //@include media-breakpoint-up(xxl) { font-size: 25.25rem; } // 1400px (404px)
}
</style>
