<script setup lang="ts">
import { ref } from 'vue'
import arrow from "../assets/arrow.svg";

const props = defineProps({
    title: String,
    right: Boolean
})

let show = ref(false)
let active = ref(false)
</script>

<template>
    <div class="slide-block__container">
        <div class="slide-block" :class="{ right, show, active }">
            <div class="slide-block__trigger" @click="() => { show = !show; active = !show }">
                <img :src="arrow" alt="arrow">
                <span>{{ title }}</span>
            </div>
            <div class="slide-block__content">
                <slot />
            </div>
        </div>
    </div>
</template>

<style scoped lang="scss">
.slide-block {
    padding: 30px;
    background-color: $light;
    position: relative;
    width: fit-content;
    transform: translate(-100%);
    transform-style: preserve-3d;

    &.active {
        animation: hide-left 1s ease-in-out;
    }

    &__container {
        width: 45%;
        margin-bottom: 20px;
    }

    &__trigger {
        display: flex;
        align-content: center;
        background-color: $black;
        border: 1px solid $light;
        border-bottom: none;
        padding: 10px 20px 10px 10px;
        font-size: 20px;
        position: absolute;
        top: 0;
        right: 0;
        transform: translate(100%, -100%) rotate(90deg);
        transform-origin: left bottom;
        cursor: pointer;
        transition-delay: .3s;
        color: $white;

        img {
            margin-right: 15px;
            transform: rotate(90deg);
            transition-delay: .3s;
        }

        span {
            white-space: nowrap;
        }
    }

    &:before {
        content: '';
        position: absolute;
        bottom: 0;
        right: 0;
        border-bottom: 20px solid $dark;
        border-left: 20px solid $light;
        width: 0;
    }

    &.right {
        float: right;
        transform: translate(100%);

        &:before {
            border-bottom: 20px solid $dark;
            border-right: 20px solid $light;
            border-left: none;
            left: 0;
            right: auto;
        }

        &.active {
            animation: hide-right 1s ease-in-out;
        }

        .slide-block {
            &__trigger {
                right: auto;
                left: 0;
                transform: rotate(90deg);
                transform-origin: left top;
                border-top: none;
                border-bottom: 1px solid $light;

                img {
                    transform: rotate(-90deg);
                }
            }
        }

        &.show {
            animation: show-right 1s ease-in-out;
            transform: translate(0);

            @keyframes show-right {
                from {
                    transform: translate(100%);
                }
                30% {
                    transform: translate(150%);
                }
                to {
                    transform: translate(0);
                }
            }

            .slide-block__trigger {
                flex-direction: row;
                transform: rotate(0) translateX(-50px) translateZ(-10px);
                border: none;

                img {
                    transform: rotate(180deg);
                }
            }
        }

        @keyframes hide-right {
            from {
                transform: translate(0);
            }
            30% {
                transform: translate(150%);
            }
            to {
                transform: translate(100%);
            }
        }
    }

    &.show {
        animation: show-left 1s ease-in-out;
        transform: translate(0);

        .slide-block__trigger {
            transform: translateX(50px) translateZ(-10px) rotate(180deg);
            transform-origin: center;
            border: none;

            img {
                transform: rotate(180deg);
            }
        }

        @keyframes show-left {
            from {
                transform: translate(-100%);
            }
            30% {
                transform: translate(-150%);
            }
            to {
                transform: translate(0);
            }
        }
    }

    @keyframes hide-left {
        from {
            transform: translate(0);
        }
        30% {
            transform: translate(-150%);
        }
        to {
            transform: translate(-100%);
        }
    }
}
</style>
