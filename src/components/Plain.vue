<script setup lang="ts">
import { ref } from 'vue'

const props = defineProps({
    title: String,
    data: String,
})
</script>

<template>
    <div class="plain">
        <div class="plain__header">
            {{ title }}
        </div>
        <div class="plain__content">
            {{ data }}
        </div>
    </div>
</template>

<style scoped lang="scss">
.plain {
    &__header {
        font-size: 30px;
        margin-bottom: 24px;
    }

    &__content {
        user-modify: read-write-plaintext-only;
        -webkit-user-modify: read-write-plaintext-only;
    }
}
</style>
