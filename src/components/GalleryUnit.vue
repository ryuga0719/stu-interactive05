<template>
  <div
    class="group h-48 md:h-80 flex items-end bg-black overflow-hidden rounded-lg shadow-lg relative cursor-pointer opacity-20 hover:opacity-100 duration-300"
  >
    <img
      :src="src"
      loading="lazy"
      :alt="title"
      class="w-full h-full object-cover absolute img-position blur-sm hover:blur-none"
      @mouseover="rollOverAction"
      @mouseleave="rollOutAction"
    />
    <span
      class="inline-block text-white text-sm md:text-lg relative ml-4 md:ml-5 mb-3"
      >{{ title }}</span
    >
  </div>
</template>

<script setup>
import GalleryMock from "../mock/GalleryMock";
import { gsap } from "gsap";
import { ref } from "vue";
const props = defineProps({
  title: String,
  src: String,
});

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
</script>

<style></style>
