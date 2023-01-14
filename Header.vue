<template>
  <div class="drawer min-h-screen">
    <input id="drawer-2137" type="checkbox" class="drawer-toggle" />
    <div id="main" class="drawer-content flex flex-col">
      <header>
        <nav class="w-full navbar bg-base-300">
          <div class="flex-none lg:hidden">
            <label for="drawer-2137" class="btn btn-square btn-ghost">
              <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"
                class="inline-block w-6 h-6 stroke-current">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16">
                </path>
              </svg>
            </label>
          </div>
          <div class="flex-1 px-2 mx-2">
            <nuxt-link to="/">
              <h1 class="font-bold underline decoration-sky-500/30 decoration-2 underline-offset-4">Music info 🎧</h1>
            </nuxt-link>
          </div>
          <div class="flex-none hidden lg:block">
            <ul class="menu menu-horizontal" slot="links">
              <li>
                <nuxt-link to="/genres">Genres</nuxt-link>
              </li>
              <li>
                <nuxt-link to="/artists">Artists</nuxt-link>
              </li>
              <li>
                <nuxt-link to="/top">TOP Tracks</nuxt-link>
              </li>
              <li>
                <nuxt-link to="/albums">Albums</nuxt-link>
              </li>
            </ul>
          </div>
        </nav>
      </header>
      <slot />
    </div>
    <div class="drawer-side">
      <label for="drawer-2137" class="drawer-overlay"></label>
      <ul class="menu p-4 w-80 bg-base-100">
        <li>
          <nuxt-link to="/genres">Genres</nuxt-link>
        </li>
        <li>
          <nuxt-link to="/artists">Artists</nuxt-link>
        </li>
        <li>
          <nuxt-link to="/top">TOP Tracks</nuxt-link>
        </li>
        <li>
          <nuxt-link to="/albums">Albums</nuxt-link>
        </li>
      </ul>
    </div>
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

  .menu {
    column-gap: 20px;
  }
}
</style>