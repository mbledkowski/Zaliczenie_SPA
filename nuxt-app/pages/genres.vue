<template>
  <div v-if="data">
    <h1>Genres</h1>
    <ul>
      <li v-for="genre in data.data" :key="genre.id">
        <nuxt-link :to="`/genres/${genre.id}`">{{ genre.name }}</nuxt-link>
        <img :src="genre.picture" alt="{{genre.name}} genre image" />
      </li>
    </ul>
  </div>
</template>

<style lang="scss" scoped>
div {
  display: flex;
  flex-flow: column nowrap;
  h1 {
    margin: 0;
    font-size: 1.5rem;
  }
  ul {
    display: flex;
    flex-flow: row wrap;
    align-items: center;
    list-style: none;
    padding: 0;
    li {
      display: flex;
      flex-direction: column;
      align-items: center;
      margin: 1rem;
      img {
        width: 100px;
        height: 100px;
      }
    }
  }
}
</style>

<script lang="ts" setup>
const { data } = await useFetch<{
  data: { id: number; name: string; picture: string }[];
}>(() => "https://api.deezer.com/genre");
</script>
