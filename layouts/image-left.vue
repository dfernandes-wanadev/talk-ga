<script setup lang="ts">
import { computed } from 'vue'
import { handleBackground } from '../layoutHelper'
import LayoutFooter from '../components/LayoutFooter.vue'

const props = defineProps({
    image: {
        type: String,
    },
    class: {
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
    <div class="grid grid-cols-2 w-full h-full auto-rows-fr">
        <div class="w-full h-full" :style="style" />
        <div class="slidev-layout default" :class="props.class">
            <slot />
        </div>
    </div>
    <LayoutFooter class="absolute bottom-0 left-0 pb-2 pl-5 pr-5" />
</template>