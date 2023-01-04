<template>
  <div v-if="genre">
    <h1>Genre</h1>
    <h2>
      {{ genre.name }}
    </h2>
    <img :src="`https://source.unsplash.com/512x512/?${genre.name.split(' ').join('-')}-music`" />
    <p v-html="genre.wiki.content">
    </p>
  </div>
  <div v-else>Please refresh the webpage!</div>
</template>

<script lang="ts" setup>
const route = useRoute();
const {data: genresData} = await useFetch<{tag: { name: string; count: number; reach: number; wiki: {summary: string; content: string;}
}}>(() => `https://ws.audioscrobbler.com/2.0/?method=tag.getinfo&tag=${route.params.id}&api_key=e2ec98b041891e5f1163138c3515c552&format=json`);
const genre = genresData.value?.tag;
</script>
