<script setup lang="ts">

const props = defineProps<{
    ad: string | undefined;
}>();

console.log(props.ad)
</script>

<template>
    <div :class="`bg-${props.ad} text-white`">
        Más información
    </div>
</template>

<style scoped>
  
</style>
