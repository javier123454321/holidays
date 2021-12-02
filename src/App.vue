<template>
  <nav
    class="px-12 py-8 bg-red-100 w-screen -mb-24 z-50 relative flex justify-end"
  >
    <router-link to="Login" class="font-bold text-red-500">Sign In</router-link>
  </nav>
  <div class="pt-24 z-10 block">
    <router-view class="" />
  </div>
</template>

<style></style>
