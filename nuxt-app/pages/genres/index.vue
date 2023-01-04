<template>
  <div v-if="genres">
    <h1 class="text-5xl font-bold m-12">Genres</h1>
    <div class="m-9 flex flex-col flex-nowrap items-center">
      <ul class="flex flex-row flex-wrap justify-between items-stretch">
        <li v-for="genre in genres" :key="genre.name" class="m-3">
          <nuxt-link :to="`/genres/${genre.name}`">
            <div class="card w-48 bg-base-100 shadow-xl min-h-full">
              <figure>
                <img :src="`https://source.unsplash.com/512x512/?${genre.name.split(' ').join('-')}-music`"
                  :alt="`${_.capitalize(genre.name)} genre image`" height="256" width="256" />
              </figure>
              <div class="card-body items-center text-center">
                <h2 class="card-title">{{ _.capitalize(genre.name) }}</h2>
              </div>
            </div>
          </nuxt-link>
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
async function getGenres(page: number) {
  const { data: genresData } = await useFetch<{
    toptags: { tag: { name: string; count: number; reach: number; }[] };
  }>(() => `https://ws.audioscrobbler.com/2.0/?method=tag.getTopTags&offset=${page * 50}&api_key=e2ec98b041891e5f1163138c3515c552&format=json`);
  const genres = genresData.value?.toptags?.tag;
  return genres
}
const genres = ref(await getGenres(page.value));
watch(page, async (page) => {
  genres.value = await getGenres(page);
})
</script>