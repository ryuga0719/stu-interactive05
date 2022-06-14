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
        <div
          class="group h-48 md:h-80 flex items-end bg-black overflow-hidden rounded-lg shadow-lg relative cursor-pointer opacity-20 hover:opacity-100 duration-300"
          v-for="(item, index) in galleryData"
          :key="index"
        >
          <img
            :src="item.src"
            loading="lazy"
            :alt="item.title"
            class="w-full h-full object-cover absolute img-position blur-sm hover:blur-none"
            @mouseover="rollOverAction"
            @mouseleave="rollOutAction"
          />
          <span
            class="inline-block text-white text-sm md:text-lg relative ml-4 md:ml-5 mb-3"
            >{{ item.title }}</span
          >
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import GalleryMock from "../mock/GalleryMock";
import { gsap } from "gsap";
import { ref } from "vue";
export default {
  setup() {
    // モックデータ
    const galleryData = GalleryMock.galleryData;

    // フラグ
    let isOver = ref(false); // マウスが要素の上に載っているか否か
    let isPlaying = ref(false); // アニメーションが再生中か否か

    // ロールオーバー
    const rollOverAction = (e) => {
      isOver.value = true;
      if (!isPlaying.value) {
        startRollOver(e);
      }
    };

    // ロールアウト
    const rollOutAction = (e) => {
      isOver.value = false;
      if (!isPlaying.value) {
        startRollOut(e);
      }
    };

    // ロールオーバーのアニメーション
    const startRollOver = (e) => {
      isPlaying.value = true;
      gsap.to(e.target, {
        objectPosition: "100% center",
        duration: 8,
        ease: "Power4.out",
        onComplete: completeRollOver(e),
      });
    };

    // ロールアウトのアニメーション
    const startRollOut = (e) => {
      isPlaying.value = true;
      gsap.to(e.target, {
        objectPosition: "0% center",
        duration: 8,
        ease: "Power4.out",
        onComplete: completeRollOut(e),
      });
    };

    // ロールオーバーのアニメーションの終わり
    const completeRollOver = (e) => {
      isPlaying.value = false;
      if (!isOver.value) {
        startRollOut(e);
      }
    };

    // ロールアウトのアニメーションの終わり
    const completeRollOut = (e) => {
      isPlaying.value = false;
      if (isOver.value) {
        startRollOver(e);
      }
    };

    return {
      galleryData,
      rollOverAction,
      rollOutAction,
    };
  },
};
</script>

<style lang="scss">
.img-position {
  object-position: 0% center;
}
</style>
