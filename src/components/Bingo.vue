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
}
</style>
