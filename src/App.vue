<script setup>
console.log(import.meta.env);
</script>

<template>
  <router-view></router-view>
  <!-- <button class="bg-purple-500 text-indigo-500">按钮</button> -->
</template>

<style >
body {
  @apply bg-gray-100;
}
#nprogress .bar {
  background-color: #fff;
  height: 3px !important;
}
</style>
