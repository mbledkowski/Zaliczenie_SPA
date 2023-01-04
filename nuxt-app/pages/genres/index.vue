<template>
  <div v-if="genres">
    <h1 class="text-5xl font-bold m-12">Genres</h1>
    <div class="m-12">
    <ul>
      <li v-for="genre in genres" :key="genre.name" class="m-6">
        <nuxt-link :to="`/genres/${genre.name}`">
          <div class="card w-48 bg-base-100 shadow-xl">
            <figure>
              <img :src="`https://source.unsplash.com/512x512/?${genre.name.split(' ').join('-')}-music`"
                :alt="`${_.capitalize(genre.name)} genre image`" height="256" width="256"/>
            </figure>
            <div class="card-body items-center text-center">
              <h2 class="card-title">{{ _.capitalize(genre.name) }}</h2>
            </div>
          </div>
        </nuxt-link>
      </li>
    </ul></div>
  </div>
  <div v-else>Please refresh the webpage!</div>
</template>

<script lang="ts" setup>
import _ from "lodash";
const { data: genresData } = await useFetch<{
  toptags: { tag: { name: string; count: number; reach: number; }[] };
}>(() => "https://ws.audioscrobbler.com/2.0/?method=tag.getTopTags&api_key=e2ec98b041891e5f1163138c3515c552&format=json");
const genres = genresData.value?.toptags?.tag;
</script>

<style lang="scss" scoped>
ul {
  display: flex;
  flex-flow: row wrap;
  justify-content: center;
}
</style>