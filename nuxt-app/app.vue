<template>
  <div id="main">
    <Header />
    <main>
      <NuxtPage />
    </main>
    <Footer />
  </div>
</template>

<style lang="scss">
#main {
  min-height: 100vh;
  display: grid;
  grid-template-rows: auto 1fr auto;
  grid-template-areas:
    "header"
    "main"
    "footer";
  main {
    display: flex;
    justify-content: center;
    align-items: center;
  }
}
</style>
