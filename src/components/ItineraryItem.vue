<script setup>
defineProps({
  showFiles: Boolean,
  fileUrl: String,
  showCost: Boolean
})
</script>

<template>
  <div class="max-w-3xl ml-auto mr-auto flex mb-3">
    <!-- Itinerary type icon -->
    <div class="w-8">
      <slot name="icon"></slot>
    </div>
    <!-- Itinerary item details and cost-->
    <div class="max-w-full">
      <slot name="details"></slot>&nbsp;
      <span v-if="showCost" class="bg-gray-300 rounded-3xl pl-2 pr-2 pt-1 pb-1 text-xs font-semibold inline-flex align-middle"><slot name="cost"></slot></span>
    </div>
    <!-- File icon -->
    <div v-if="showFiles && fileUrl.length" class="w-6 ml-auto order-2 pl-3 cursor-pointer">
      <a href="/src/icons/IconCommunity.vue"><i class="fa-solid fa-file"></i></a>
    </div>
  </div>
  <!-- Divider line -->
  <div class="border-b-2 border-gray-300 mt-3 mb-3 max-w-3xl ml-auto mr-auto"></div>
    
</template>

<style scoped>

</style>
