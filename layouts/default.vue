<template>
    <div class="slidev-layout bg-main">
        <div class="my-auto">
            <slot />
        </div>
        <LayoutFooter class="absolute bottom-0 left-0 pb-2 pl-5 pr-5" />
    </div>
</template>

<script setup lang="ts">
import LayoutFooter from "../components/LayoutFooter.vue";

</script>