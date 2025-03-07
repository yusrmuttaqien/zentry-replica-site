<script setup lang="ts">
import gsap from "gsap";
import loop from "~/assets/audio/loop.mp3";

const isNavVisible = ref(false);
const isAudioPlaying = ref(false);
const isAudioIndicated = ref(false);
const container = ref<HTMLElement | null>(null);
const audio = ref<HTMLAudioElement | null>(null);

const navItems = ["Nexus", "Prolouge", "Vault", "About", "Contact"];
let gsapTo: ReturnType<typeof gsap.to>;
const controller = new AbortController();
const bars = [1, 2, 3, 4];
let lastScrollY = 0;

function toggleAudio() {
  const isPlaying = !isAudioPlaying.value;
  isAudioPlaying.value = isPlaying;
  isAudioIndicated.value = isPlaying;

  if (isPlaying) {
    audio.value?.play();
  } else {
    audio.value?.pause();
  }
}
function handleScroll(progress: number, direction: "up" | "down") {
  if (progress === 0) {
    isNavVisible.value = true;
    container.value?.classList.remove("floating-nav");
  } else if (direction === "up") {
    isNavVisible.value = true;
    container.value?.classList.add("floating-nav");
  } else {
    isNavVisible.value = false;
    container.value?.classList.add("floating-nav");
  }

  gsapTo?.kill();
  gsapTo = gsap.to(container.value, {
    y: isNavVisible.value ? 0 : -100,
    opacity: isNavVisible.value ? 1 : 0,
    duration: 0.1,
  });
}

onMounted(() => {
  window.addEventListener(
    "scroll",
    () => {
      const scrollY = window.scrollY;

      handleScroll(scrollY, scrollY > lastScrollY ? "down" : "up");

      lastScrollY = scrollY;
    },
    { signal: controller.signal },
  );
  handleScroll(lastScrollY, "down");
});
onBeforeUnmount(() => {
  controller.abort();
});
</script>

<template>
  <div
    ref="container"
    class="fixed inset-x-0 top-4 z-50 h-16 border-none transition-all duration-700
      sm:inset-x-6"
  >
    <nav class="flex size-full items-center justify-between p-4">
      <div class="flex items-center gap-7">
        <img src="~/assets/img/logo.png" alt="logo" class="w-10" />
        <UiButton
          id="product-button"
          class="hidden items-center justify-center gap-1 bg-blue-50 md:flex"
        >
          <template #text>Products</template>
          <template #icon-right>
            <IconArrowRight class="-m-2 text-3xl" />
          </template>
        </UiButton>
      </div>
      <div class="flex h-full items-center">
        <div class="hidden md:block">
          <a
            :key="item"
            class="nav-hover-btn"
            v-for="item in navItems"
            :href="`#${item.toLowerCase()}`"
          >
            {{ item }}
          </a>
        </div>
        <button
          @click="toggleAudio"
          class="ml-10 flex cursor-pointer items-center space-x-0.5"
        >
          <audio loop ref="audio" class="hidden" :src="loop" />
          <div
            :key="bar"
            v-for="bar in bars"
            :style="{ animationDelay: `${bar * 0.1}s` }"
            :class="['indicator-line', { active: isAudioIndicated }]"
          />
        </button>
      </div>
    </nav>
  </div>
</template>
