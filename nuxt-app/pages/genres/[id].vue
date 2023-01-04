<template>
  <div v-if="genre">
    <h1>Genre</h1>
    <h2>
      {{ genre.name }}
      <span class="gray">
        {{ genre.id }}
      </span>
    </h2>
    <img :src="genre.picture_xl" />
  </div>
  <div v-else>Please refresh the webpage!</div>
</template>

<script lang="ts" setup>
const route = useRoute();
const { data: genre } = await useFetch<{
  id: number;
  name: string;
  picture_xl: string;
}>(() => `https://api.deezer.com/genre/${route.params.id}`);
</script>
