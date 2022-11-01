<script setup lang="ts">
import SlideBlock from './components/SlideBlock.vue'
import List from './components/List.vue'
import Like from './components/Like.vue'
import Plain from './components/Plain.vue'

const blocks = [
    {
        title: 'Shopping list',
        component: List,
        data: ['MILK', 'BREAD', 'HAM', 'CHEESE', 'WATER']
    },
    {
        title: 'KITTY',
        component: Like,
    },
    {
        title: 'MAMAAA OOOO',
        component: Plain,
        data: `THIS ONE IS NOT A LIST - JUST SOME PLAIN OL’ TEXT.

IS THIS THE REAL LIFE
IS THIS JUST FANTASY
CAUGHT IN A LANDSIDE
NO ESCAPE FROM REALITY

BY THE WAY IF THERE WAS A REALLY LONG LINE, I’M PRETTY SURE AT SOME POINT IT WOULD WRAP TO THE NEXT LINE. JUST LIKE THE OTHER ELEMENTS ON THIS PAGE, THIS ONE HAS A PRE-DEFINED MAX-WIDTH`
    },
    {
        title: 'Books to read',
        component: List,
        data: ['SAPIENS BY YUVAL NOAH HARARI', 'THE THEORY OF EVERYTHING BY STEPHEN HAWKING', 'A WILD SHEEP CHASE BY HARUKI MURAKAMI', 'CLEAN CODE BY ROBERT MARTIN']
    },
]
</script>

<template>
  <div class="main">
    <SlideBlock v-for="(block, key) in blocks" :key="key" :title="block.title" :right="!!(key % 2)">
        <component :is="block.component" :data="block.data" :title="block.title" />
    </SlideBlock>
  </div>
</template>

<style scoped lang="scss">
.main {
  background: $dark;
  width: 100%;
  height: 100vh;
  font-size: 20px;
  font-family: sans-serif;
  text-transform: uppercase;

    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    align-content: space-between;

    padding: 40px 0;
}
</style>
