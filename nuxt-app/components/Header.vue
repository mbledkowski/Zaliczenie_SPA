<template>
  <header>
    <nuxt-link to="/"><h1>Deezer API front-end</h1></nuxt-link>
    <nav>
      <nuxt-link to="/genres">Genres</nuxt-link>
    </nav>
  </header>
</template>

<style lang="scss" scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem;
  background-color: #f5f5f5;
  border-bottom: 1px solid #ccc;
  h1 {
    margin: 0;
    font-size: 1.5rem;
  }
  nav {
    a {
      margin-left: 1rem;
    }
  }
}
</style>
