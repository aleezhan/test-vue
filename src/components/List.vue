<script setup lang="ts">
import { ref, computed } from 'vue'

const props = defineProps({
    title: String,
    data: Array,
})

const checked = ref({})
const checkedLength = computed((): number => Object.keys(checked.value).length);

</script>

<template>
    <div class="list">
        <div class="list__header">{{ title }} [{{ checkedLength }}/{{ data.length }}]</div>
        <ul class="list">
            <li v-for="(item, key) in data" :key="key" :class="{ checked: checked[item] }" class="list__item" @click="checked[item] = !checked[item]">{{ item }}</li>
        </ul>
    </div>
</template>

<style scoped lang="scss">
.list {
    &__header {
        font-size: 30px;
        margin-bottom: 24px;
    }

    ul {
        padding-left: 20px;
    }

    &__item {
        cursor: pointer;
        margin-bottom: 6px;

        &.checked {
            text-decoration: line-through;
        }
    }
}
</style>
