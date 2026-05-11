<script setup lang="ts">
const props = defineProps<{
    adsButton: boolean;
}>();
</script>

<template>
    <div v-show="!props.adsButton" class="position-fixed top-50 start-50 translate-middle text-center fs-text_12xl">
        <p>43</p>
    </div>
</template>

<style scoped>
  
</style>
