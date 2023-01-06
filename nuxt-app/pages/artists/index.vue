<template>
  <section class="container mx-auto px-4 py-4" v-if="artist">
    <ul class="grid grid-cols-4 gap-10">
      <li class="bg-white" v-for="a in artist" :key="a.name">
          <div class="max-w-sm rounded overflow-hidden shadow-lg">
            <img class="w-full" :src="a.image[2]['#text']" :alt="a.image[2].size">
            <div class="px-6 py-5">
              <div class="font-bold text-xl mb-2">Artist : {{a.name}}</div>
              <p class="py-2 text-gray-700 text-sm">
                listeners: {{a.listeners}}
              </p>
              <a class=" text-blue-600" :href="a.url">Website: {{a.name}}</a>
            </div>
            <div class="px-6 pt-4 pb-2">
              <span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-2">#photography</span>
              <span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-2">#travel</span>
              <span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-2">#winter</span>
            </div>
          </div>
      </li>
    </ul>
  </section>
</template>

<script setup>

  import {useFetch} from "#app";

  definePageMeta({
    layout: 'artists'
  })
  const {data: artistData } = await useFetch(`https://ws.audioscrobbler.com/2.0/?method=geo.gettopartists&country=spain&api_key=e2ec98b041891e5f1163138c3515c552&format=json`)

  const artist = artistData._rawValue.topartists.artist;

</script>

<style scoped>

</style>