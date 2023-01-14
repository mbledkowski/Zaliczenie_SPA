<template>
  <div v-if="albums">
    <h1 class="text-5xl font-bold m-12">Top albums</h1>
    <div class="m-9 flex flex-col flex-nowrap items-center">
      <ul class="flex flex-row flex-wrap justify-between items-stretch">
        <li v-for="al in albums" class="m-3">
          <div class="card w-48 bg-base-100 shadow-xl min-h-full">
            <!-- <figure>
              <img :src="`https://source.unsplash.com/512x512/?${al.artist.name.split(' ').join('-')}-music`"
                :alt="`${_.capitalize(al.name)} al image`" height="256" width="256" />
            </figure> -->
            <div class="card-body items-center text-center">
              <nuxt-link :to="`/albums/${al.name}`">
                <h2 class="card-bordered rounded-md p-3 leading-5 hover:underline decoration-sky-500/30 font-bold">
                  Track:<br>{{ al.name }}</h2>
              </nuxt-link>
              <nuxt-link :to="`/albums/${al.artist.name}`">
                <h2 class="card-bordered rounded-md p-3 leading-5 hover:underline decoration-sky-500/30 font-bold">
                  Artist:<br>{{ al.artist.name }}</h2>
              </nuxt-link>
              <h2 class="card-bordered rounded-md p-3 font-bold">Playcount:<br>{{ al.playcount }}</h2>
            </div>
          </div>
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

<script lang="ts" setup>

import _ from "lodash";

var artist;

const page = ref(1);
async function getTop(page: number) {
  const { data: topData } = await useFetch<{
    topalbums: { album: { name: string; }[] };
  }>(() => `https://ws.audioscrobbler.com/2.0/?method=artist.gettopalbums&artist=${artist}&${page}&api_key=e2ec98b041891e5f1163138c3515c552&format=json`);
  const albums = topData.value?.topalbums?.album
  return albums
}
const albums = ref(await getTop(page.value));
watch(page, async (page) => {
  albums.value = await getTop(page);
})
console.log(albums)
</script>