<script setup lang="ts">
import { ref } from 'vue'
import kitty from '../assets/KITTY.jpeg'

const props = defineProps({
    title: String,
})

const likes = ref([])

function random() {
    return (Math.floor(Math.random() * 100) + 1) + '%'
}
</script>

<template>
    <div class="like">
        <div class="like__header">{{ title }}</div>
        <div class="like__image">
            <img :src="kitty" alt="image for like">
            <span v-for="(like, key) in likes" :key="key" class="like__image_likes" :style="{ left: like[0], top: like[1] }">❤</span>
        </div>
        <button @click="likes.push([random(), random()])">AWW :3</button>
    </div>
</template>

<style scoped lang="scss">
.like {
    &__header {
        font-size: 30px;
        margin-bottom: 24px;
    }

    .like__image {
        position: relative;

        img {
            display: block;
            width: 200px;
            margin-bottom: 15px;
        }

        &_likes {
            position: absolute;
            color: red;
            font-size: 40px;
            transform: translateY(-50%);
            animation: show-like .8s ease-out;

            @keyframes show-like {
                from {
                    opacity: 0;
                    transform: translateY(0);
                }
                to {
                    opacity: 1;
                    transform: translateY(-50%);
                }
            }
        }
    }

    button {
        background-color: $black;
        border-radius: 5px;
        width: 100%;
        font-size: 20px;
        padding: 5px 0;
        cursor: pointer;
        border: none;
        outline: none;
        color: $white;
    }
}
</style>
