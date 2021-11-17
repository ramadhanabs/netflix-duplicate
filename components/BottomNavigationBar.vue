<template>
  <div class="grid grid-cols-3 bg-gray-900 border-t border-gray-700 px-5 py-5 font-poppins text-xs font-normal text-gray-500 text-center fixed bottom-0 max-w-screen-sm w-full">
    <nuxt-link to="/">
    <div class="hover:text-white">
      <div class="mb-2">
        <font-awesome-icon :icon="['fas', 'home']" class="text-2xl mx-6"  />
      </div>
      <p>Home</p>
    </div>
    </nuxt-link>
    <nuxt-link to="/categories">
    <div class="hover:text-white">
      <div class="mb-2">
        <font-awesome-icon :icon="['fas', 'film']" class="text-2xl mx-6"  />
      </div>
      <p>Categories</p>
    </div>
    </nuxt-link>
    <nuxt-link to="/search">
      <div class="hover:text-white">
        <div class="mb-2">
          <font-awesome-icon :icon="['fas', 'search']" class="text-2xl text-center"  />
        </div>
        <p>Search</p>
      </div>
    </nuxt-link>
  </div>
</template>
