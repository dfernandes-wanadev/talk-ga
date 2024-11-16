<template>
    <default class="intro">
        <img v-if="eventImageSrc" :src="eventImageSrc" class="rounded-full p-2 absolute top-5 right-5" height="125"
            width="125" />
        <div class="flex items-center">
            <figure class="w-1/2 px-12 relative">
                <img :src="imageSrc" height="312" width="312" class="rounded-full p-2 bg-gradient-to-r from-[#6441db]
    via-[#964be6] to-[#ff5dff] dark:(from-white to-purple-50)" />

                <img v-if="subjectImageSrc" :src="subjectImageSrc"
                    class="rounded-full p-2 absolute top-0 right-5 bg-gradient-to-r from-[#6441db] via-[#964be6] to-[#ff5dff] dark:(from-white to-purple-50)"
                    height="150" width="150" />
            </figure>
            <div class="w-1/2">
                <slot />
            </div>
        </div>
    </default>
</template>

<script setup lang="ts">
import { computed } from "vue";
import { resolveAssetUrl } from "../layoutHelper";
import Default from "../layouts/default.vue";

const props = defineProps({
    introImage: {
        type: String,
    },
    subjectImage: {
        type: String,
        default: "",
    },
    eventImage: {
        type: String,
        default: "",
    },
});
const imageSrc = computed(() => resolveAssetUrl(props.introImage));
const subjectImageSrc = computed(() => resolveAssetUrl(props.subjectImage));
const eventImageSrc = computed(() => resolveAssetUrl(props.eventImage));
</script>