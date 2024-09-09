<script setup>

</script>

<template>
  <div class="mt-12 mb-4 rounded-lg bg-gray-100 p-2 max-w-3xl mr-auto ml-auto">
    <!-- <div class="border-b-2 border-gray-500 mt-12 ml-5 mr-5 mb-3 rounded"></div> -->
    <h1 class="text-center font-bold text-xl">
      <slot name="date"></slot>
    </h1>
    <h2 class="text-center text-lg">
      <slot name="countries"></slot>
    </h2>
    <!-- <div class="border-b-2 border-gray-400 mt-3 mb-3 max-w-3xl ml-auto mr-auto"></div> -->
  </div>
    
</template>

<style scoped>

</style>
