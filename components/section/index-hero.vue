<script setup lang="ts">
import gsap from "gsap";
import { ScrollTrigger } from "gsap/all";
import type { VNode } from "vue";

const isLoading = ref(true);
const currentIndex = ref(1);
const loadedVideos = ref(0);
const hasClicked = ref(false);
const nextVideo = ref<HTMLVideoElement | null>(null);
const nextVideoIndex = computed(() => (currentIndex.value % totalVideos) + 1);

const totalVideos = 4;
let gsapCtx: ReturnType<typeof gsap.context>;

function handleMiniVideoClick() {
  currentIndex.value = nextVideoIndex.value;
  hasClicked.value = true;
}
function getVideoSrc(index: number) {
  return `/videos/hero-${index}.mp4`;
}
function handleVideoLoad() {
  loadedVideos.value += 1;
}
function checkVideoLoaded(node: VNode<HTMLVideoElement>) {
  const isEnoughData = node.el?.readyState || 0 >= 3;

  if (isEnoughData) loadedVideos.value += 1;
}
function animateCycle() {
  gsap.set("#next-video", { visibility: "visible" });
  gsap.to("#next-video", {
    transformOrigin: "center",
    scale: 1,
    width: "100%",
    height: "100%",
    duration: 1,
    ease: "power1.inOut",
    onStart() {
      nextVideo.value?.play();
    },
  });
  gsap.from("#current-video", {
    transformOrigin: "center",
    scale: 0,
    duration: 1,
    ease: "power1.inOut",
  });
}
function animateScroll() {
  gsap.set("#video-frame", {
    clipPath: "polygon(14% 0, 72% 0, 88% 90%, 0 95%)",
    borderRadius: "0% 0% 40% 10%",
  });
  gsap.from("#video-frame", {
    clipPath: "polygon(0% 0%, 100% 0%, 100% 100%, 0% 100%)",
    borderRadius: "0% 0% 0% 0%",
    ease: "power1.inOut",
    scrollTrigger: {
      trigger: "#video-frame",
      start: "center center",
      end: "bottom center",
      scrub: true,
    },
  });
}

onMounted(() => {
  gsap.registerPlugin(ScrollTrigger);

  animateScroll();
});
watch([hasClicked, currentIndex], () => {
  if (!gsapCtx) {
    gsapCtx = gsap.context((self) => {
      self.add("play", animateCycle);
      animateCycle();
    });
  } else {
    gsapCtx.revert();
    gsapCtx.play();
  }
});
watchEffect(() => {
  if (loadedVideos.value === totalVideos - 1) {
    isLoading.value = false;
  }
});
</script>

<template>
  <section class="relative h-dvh overflow-x-hidden">
    <div
      v-if="isLoading"
      class="flex-center absolute z-[100] h-dvh w-screen overflow-hidden bg-violet-50"
    >
      <div class="three-body">
        <div class="three-body__dot"></div>
        <div class="three-body__dot"></div>
        <div class="three-body__dot"></div>
      </div>
    </div>
    <div
      id="video-frame"
      class="bg-blue-75 relative z-10 size-full overflow-hidden rounded-lg"
    >
      <div>
        <div
          class="mask-clip-path absolute-center absolute z-50 size-64 cursor-pointer
            overflow-hidden rounded-lg"
        >
          <div
            @click="handleMiniVideoClick"
            class="origin-center scale-50 opacity-0 transition-all ease-in hover:scale-100
              hover:opacity-100"
          >
            <video
              loop
              muted
              ref="nextVideo"
              id="current-video"
              @loadeddata="handleVideoLoad"
              @vue:mounted="checkVideoLoaded"
              :src="getVideoSrc(nextVideoIndex)"
              class="size-64 origin-center scale-150 object-cover object-center"
            />
          </div>
        </div>

        <video
          loop
          muted
          id="next-video"
          ref="nextVideo"
          @loadeddata="handleVideoLoad"
          @vue:mounted="checkVideoLoaded"
          :src="getVideoSrc(currentIndex)"
          class="absolute-center invisible z-20 size-64 object-cover object-center"
        />

        <video
          loop
          muted
          autoplay
          @loadeddata="handleVideoLoad"
          @vue:mounted="checkVideoLoaded"
          :src="getVideoSrc(currentIndex)"
          class="absolute top-0 left-0 size-full object-cover object-center"
        />
      </div>

      <h1 class="font-zentry hero-heading text-blue-75 absolute bottom-5 z-40">
        G<span class="special-font">a</span>ming
      </h1>

      <div class="absolute top-0 left-0 z-40 size-full">
        <div class="mt-24 px-5 sm:px-10">
          <h1 class="hero-heading text-blue-100">
            Redefi<span class="special-font">n</span>e
          </h1>
          <p class="font-robert mb-5 ml-[0.1em] max-w-64 text-blue-100">
            Enter the Metagame Layer <br />
            Unleash the Play Economy
          </p>
          <UiButton
            id="watch-trailer"
            title="Watch trailer"
            class="gap-3 bg-yellow-300"
          >
            <template #icon-left>
              <IconArrowRight class="-m-2 text-3xl" />
            </template>
            <template #text>Watch trailer</template>
          </UiButton>
        </div>
      </div>
    </div>

    <h1 class="font-zentry hero-heading absolute bottom-5 text-black">
      G<span class="special-font">a</span>ming
    </h1>
    <div class="absolute top-24 px-5 sm:px-10">
      <h1 class="hero-heading text-black">
        Redefi<span class="special-font">n</span>e
      </h1>
    </div>
  </section>
</template>
