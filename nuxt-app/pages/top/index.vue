<template>
  <div v-if="top">
    <h1 class="text-5xl font-bold m-12">TOP played songs</h1>
    <div class="m-9 flex flex-col flex-nowrap items-center">
      <ul class="flex flex-row flex-wrap justify-between items-stretch">
        <li v-for="t in top" :key="t.name" class="m-3">
          <div class="card w-48 bg-base-100 shadow-xl min-h-full">
            <figure>
              <img :src="`https://source.unsplash.com/512x512/?${t.artist.name.split(' ').join('-')}-music`"
                :alt="`${_.capitalize(t.name)} t image`" height="256" width="256" />
            </figure>
            <div class="card-body items-center text-center">
              <nuxt-link :to="`/top/${t.name}`">
                <h2 class="card-bordered rounded-md p-3 leading-5 hover:underline decoration-sky-500/30 font-bold">
                  Track:<br>{{ t.name }}</h2>
              </nuxt-link>
              <nuxt-link :to="`/top/${t.artist.name}`">
                <h2 class="card-bordered rounded-md p-3 leading-5 hover:underline decoration-sky-500/30 font-bold">
                  Artist:<br>{{ t.artist.name }}</h2>
              </nuxt-link>
              <h2 class="card-bordered rounded-md p-3 font-bold">Playcount:<br>{{ t.playcount }}</h2>
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
</script>