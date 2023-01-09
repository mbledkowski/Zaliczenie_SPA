<template>
  <section class="container mx-auto px-5 py-10" v-if="top">
    <ul class="grid grid-cols-3 gap-10">
      <li class="bg-gradient-to-b from-gray-600 to-zinc-700 rounded-xl shadow-lg shadow-zinc" v-for="t in top">
        <div class="px-7 py-5 flex flex-col justify-center items-start">
          <div class="">Artist : {{ t.artist.name }}</div>
          <div class="">Title : {{ t.name }}</div>
          <div class="">Przesłuchane : {{ t.listeners }}</div>
          <img class="rounded-xl" :src="t.image[2]['#text']">
          <div class="text-ellipsis">{{ t.url }}</div>
        </div>
      </li>
    </ul>
  </section>
</template>

<script setup>

import { useFetch } from "#app";

definePageMeta({
  layout: 'top'
})
const { data: topSongs } = await useFetch(`https://ws.audioscrobbler.com/2.0/?method=geo.gettoptracks&country=spain&api_key=e2ec98b041891e5f1163138c3515c552&format=json`)

const top = topSongs._rawValue.tracks.track;

console.log(top);
</script>

<style scoped>

</style>