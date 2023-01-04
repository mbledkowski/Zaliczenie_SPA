<template>
  <div v-if="genres">
    <h1>Genres</h1>
    <ul>
      <li v-for="genre in genres" :key="genre.name">
        <nuxt-link :to="`/genres/${genre.name}`"
          >{{ genre.name }}
          <img :src="`https://source.unsplash.com/512x512/?${genre.name.split(' ').join('-')}-music`" alt="{{genre.name}} genre image" />
        </nuxt-link>
      </li>
    </ul>
  </div>
  <div v-else>Please refresh the webpage!</div>
</template>

<script lang="ts" setup>
const {data: genresData} = await useFetch<{
  toptags: {tag: { name: string; count: number; reach: number; }[]};
}>(() => "https://ws.audioscrobbler.com/2.0/?method=tag.getTopTags&api_key=e2ec98b041891e5f1163138c3515c552&format=json");
const genres = genresData.value?.toptags?.tag;
</script>
