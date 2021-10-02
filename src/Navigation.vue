<template>
  <div>
    <div
      style="width: max-content"
      class="flex items-center justify-center p-2 invisible sm:visible"
    >
      <button
        class="
          h-8
          w-8
          rounded-full
          bg-white bg-opacity-80
          hover:bg-opacity-100
          shadow-md
        "
        @click="$emit('prev')"
      >
        <svg viewBox="0 0 24 24" class="fill-current text-gray-500 h-8">
          <path
            d="M14.71 6.71a.9959.9959 0 00-1.41 0L8.71 11.3c-.39.39-.39 1.02 0 1.41l4.59 4.59c.39.39 1.02.39 1.41 0 .39-.39.39-1.02 0-1.41L10.83 12l3.88-3.88c.39-.39.38-1.03 0-1.41z"
          ></path>
        </svg>
      </button>
    </div>
    <pagination
      :pages="pages"
      :page="page"
      @goto="$emit('goto', $event)"
      style="width: max-content; height: max-content; top: auto"
      class="mx-auto max-w-full"
    ></pagination>
    <div
      style="width: max-content; left: auto"
      class="absolute flex items-center justify-center p-2"
    >
      <button
        class="
          h-8
          w-8
          rounded-full
          bg-white bg-opacity-80
          hover:bg-opacity-100
          shadow-md
          invisible
          sm:visible
        "
        @click="$emit('next')"
      >
        <svg viewBox="0 0 24 24" class="fill-current text-gray-500 h-8">
          <path
            d="M9.29 6.71c-.39.39-.39 1.02 0 1.41L13.17 12l-3.88 3.88c-.39.39-.39 1.02 0 1.41.39.39 1.02.39 1.41 0l4.59-4.59c.39-.39.39-1.02 0-1.41L10.7 6.7c-.38-.38-1.02-.38-1.41.01z"
          ></path>
        </svg>
      </button>
    </div>
  </div>
</template>
<script>
import Pagination from "./Pagination.vue";
export default {
  components: { Pagination },
  props: ["pages", "page"],
  emits: ["next", "prev", "goto"],
};
</script>