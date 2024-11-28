<template>
    <div :class="alertClass" role="alert" class="mt-3 relative flex w-full p-3 text-sm text-white rounded-md">
        <!-- cannot use component in slidev with carbon icons -->
        <carbon-checkmark-outline v-if="props.type === AlertType.Success" class="h-5 w-5 mr-2" />
        <carbon-error v-else-if="props.type === AlertType.Error" class="h-5 w-5 mr-2" />
        <carbon-warning v-else-if="props.type === AlertType.Warning" class="h-5 w-5 mr-2" />
        <carbon-information v-else class="h-5 w-5 mr-2" />

        <slot />
    </div>
</template>

<script setup lang="ts">
import { computed } from 'vue';

enum AlertType {
    Success = 'success',
    Warning = 'warning',
    Error = 'error',
    Info = 'info'
}

const props = defineProps<{
    type: {
        type: AlertType
        default: 'info'
    }
}>()


const alertClass = computed(() => {
    switch (props.type) {
        case AlertType.Success:
            return 'bg-green-800'
        case AlertType.Warning:
            return 'bg-yellow-800'
        case AlertType.Error:
            return 'bg-red-800'
        case AlertType.Info:
        default:
            return 'bg-blue-800'
    }
})

</script>