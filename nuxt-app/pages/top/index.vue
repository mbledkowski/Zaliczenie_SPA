<template>
  <div v-if="top">
    <h1 class="text-5xl font-bold m-12">TOP Songs</h1>
    <div class="m-9 flex flex-col flex-nowrap items-center">
      <ul class="flex flex-row flex-wrap justify-between items-stretch">
        <li v-for="t in top" :key="t.name" class="m-3">
          <!-- <nuxt-link :to="`/top/${t.name}`"> -->
          <div class="card w-48 bg-base-100 shadow-xl min-h-full">
            <figure>
              <img :src="`https://source.unsplash.com/512x512/?${t.name.split(' ').join('-')}-music`"
                :alt="`${_.capitalize(t.name)} t image`" height="256" width="256" />
            </figure>
            <div class="card-body items-center text-center">
              <h2 class="card-title">Name: {{ _.capitalize(t.name) }}</h2>
              <h2 class="card-artist">Artist: {{ _.capitalize(t.artist.name) }}</h2>
              <h2 class="card-url">Playcount: {{ _.capitalize(t.playcount) }}</h2>
            </div>
          </div>
          <!-- </nuxt-link> -->
        </li>
      </ul>
      <div class="btn-group">
        <button class="btn" @click="page--">«</button>
        <button class="btn">Page {{ page }}</button>
        <button class="btn" @click="page++">»</button>
      </div>
    </div>
  </div>
  <div v-else>Please refresh the webpage!</div>
</template>

<!-- <script setup>

import { useFetch } from "#app";

definePageMeta({
  layout: 'top',
})
const { data: topSongs } = await useFetch(`https://ws.audioscrobbler.com/2.0/?method=geo.gettoptracks&country=poland&page=2&api_key=e2ec98b041891e5f1163138c3515c552&format=json`)

const top = topSongs

console.log(top);
</script> -->
<script lang="ts" setup>
import _ from "lodash";
const page = ref(1);
async function getTop(page: number) {
  const { data: topData } = await useFetch<{
    tracks: { track: { name: string; playcount: string; url: string; artist: { name: string } }[] };
  }>(() => `https://ws.audioscrobbler.com/2.0/?method=chart.gettoptracks&page=${page}&api_key=e2ec98b041891e5f1163138c3515c552&format=json`);
  const top = topData.value?.tracks?.track;
  return top
}
const top = ref(await getTop(page.value));
watch(page, async (page) => {
  top.value = await getTop(page);
})

const { data: topSongs } = await useFetch(`https://ws.audioscrobbler.com/2.0/?method=tag.getinfo&tag=taylor+swift&api_key=e2ec98b041891e5f1163138c3515c552&format=json`)
console.log(top)
console.log(topSongs)
</script>