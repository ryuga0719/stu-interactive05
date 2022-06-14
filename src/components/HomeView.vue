<template>
  <div class="bg-white py-6 sm:py-8 lg:py-12">
    <div class="max-w-screen-2xl px-4 md:px-8 mx-auto">
      <h2
        class="text-gray-800 text-2xl lg:text-3xl font-bold text-center mb-4 md:mb-8 xl:mb-12"
      >
        Photo Gallery
      </h2>

      <div
        class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 gap-4 md:gap-6 xl:gap-8 mb-4 md:mb-8"
      >
        <a
          href="#"
          class="group h-48 md:h-80 flex items-end bg-gray-100 overflow-hidden rounded-lg shadow-lg relative"
          v-for="(item, index) in galleryData"
          :key="index"
        >
          <img
            :src="item.src"
            loading="lazy"
            :alt="item.title"
            class="w-full h-full object-cover object-center absolute"
          />
          <span
            class="inline-block text-white text-sm md:text-lg relative ml-4 md:ml-5 mb-3"
            >{{ item.title }}</span
          >
        </a>
      </div>

      <div class="flex justify-between items-start sm:items-center gap-8">
        <p class="max-w-screen-sm text-gray-500 text-sm lg:text-base">
          旅行の思い出
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import GalleryMock from "../mock/GalleryMock";
export default {
  setup() {
    const galleryData = GalleryMock.galleryData;
    return {
      galleryData,
    };
  },
};
</script>

<style></style>
