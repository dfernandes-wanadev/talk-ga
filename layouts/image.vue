<script setup lang="ts">
import { computed } from 'vue'
import { handleBackground } from '../layoutHelper'

const props = defineProps({
    image: {
        type: String,
    },
    backgroundSize: {
        type: String,
        default: 'cover',
    },
})

const style = computed(() => handleBackground(props.image, false, props.backgroundSize))
</script>

<template>
    <div class="slidev-layout w-full h-full" :style="style">
        <slot />
    </div>
    <LayoutFooter class="absolute bottom-0 left-0 pb-2 pl-5 pr-5" />
</template>
