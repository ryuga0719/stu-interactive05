<template>
  <div class="py-6 sm:py-8 lg:py-12">
    <div class="max-w-screen-2xl px-4 md:px-8 mx-auto">
      <h2
        class="text-indigo-600 text-2xl lg:text-3xl font-bold text-center mb-4 md:mb-8 xl:mb-12"
      >
        Photo Gallery
      </h2>

      <div
        class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 gap-4 md:gap-6 xl:gap-8 mb-4 md:mb-8"
      >
        <GalleryUnit
          v-for="(item, index) in galleryData"
          :key="index"
          :title="item.title"
          :src="item.src"
        />
      </div>
    </div>
  </div>
</template>

<script setup>
import GalleryMock from "../mock/GalleryMock";
import GalleryUnit from "../components/GalleryUnit.vue";
// モックデータ
const galleryData = GalleryMock.galleryData;
</script>

<style lang="scss">
.img-position {
  object-position: 0% center;
}
</style>
