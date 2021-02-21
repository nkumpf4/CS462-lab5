<template>
  <div id="app" class="min-h-screen bg-gray-100">
    <div id="nav" class="flex justify-center divide-x p-8">
      <router-link class="px-2" to="/">Home</router-link>
      <router-link class="px-2" to="/sensor-profile">
        Sensor Profile
      </router-link>
    </div>
    <router-view />
  </div>
</template>

<style>
a.router-link-exact-active {
  color: theme("colors.green.500");
}
</style>
