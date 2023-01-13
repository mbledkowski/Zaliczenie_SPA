<template>
    <div class="hero min-h-full bg-base-200 flex flex-col items-start">
        <h1 class="text-5xl font-bold m-12">Information:</h1>
        <div class="hero-content flex-col lg:flex-row m-12 p-0" v-if="t">
            <img :src="`https://source.unsplash.com/512x512/?${t.name.split(' ').join('-')}-music`"
                class="max-w-sm rounded-lg shadow-2xl" />
            <div>
                <h2 class="text-5xl font-bold">{{ _.capitalize(t.name) }}</h2>
                <p class="py-6" v-html="t.wiki.summary"></p>
            </div>
        </div>
        <div class="hero-content" v-else>Please refresh the webpage!</div>
    </div>
</template>
  
<script lang="ts" setup>
import _ from "lodash";
const route = useRoute();
const { data: tsData } = await useFetch<{
    tag: {
        name: string; count: number; reach: number; wiki: { summary: string; content: string; };
    }
}>(() => `https://ws.audioscrobbler.com/2.0/?method=tag.getinfo&tag=${route.params.id}&api_key=e2ec98b041891e5f1163138c3515c552&format=json`);
const t = tsData.value?.tag;

console.log(t)
</script>
