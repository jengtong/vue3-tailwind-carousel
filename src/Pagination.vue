<template>
  <div class="flex flex-wrap gap-2 p-2">
    <button
      v-for="i in pages"
      :key="i"
      class="h-3 w-3 rounded-full bg-white shadow-md hover:bg-opacity-100"
      @click="$emit('goto', i - 1)"
      :class="{
        'bg-opacity-60': i != page + 1,
        'bg-opacity-90 bg-yellow-500': i == page + 1,
      }"
    ></button>
  </div>
</template>
<script>
export default {
  props: ["pages", "page"],
  emits: ["goto"],
};
</script>