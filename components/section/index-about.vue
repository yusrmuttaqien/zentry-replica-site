<script setup lang="ts">
import gsap from "gsap";
import { ScrollTrigger } from "gsap/all";

const controller = new AbortController();

function timeline() {
  const clipTimeline = gsap.timeline({
    scrollTrigger: {
      trigger: "#clip",
      start: "center center",
      end: "+=800 center",
      scrub: 0.5,
      pin: true,
      invalidateOnRefresh: true,
    },
  });

  const to = clipTimeline.to(".mask-clip-path", {
    width: "100vw",
    height: "100vh",
    borderRadius: 0,
  });

  return { timeline: clipTimeline, to };
}

onMounted(() => {
  gsap.registerPlugin(ScrollTrigger);
  timeline();

  window.addEventListener(
    "resize",
    () => {
      const target = document.getElementById("clip");

      if (!target) return;
      target.children[0].removeAttribute("style");
      ScrollTrigger.refresh();
    },
    { signal: controller.signal },
  );
});

onBeforeUnmount(() => {
  controller.abort();
});
</script>

<template>
  <section id="about" class="min-h-dvh">
    <div class="relative mb-8 flex flex-col items-center gap-5 pt-36">
      <h2 class="font-general text-sm uppercase md:text-[10px]">
        Welcome to Zentry
      </h2>
      <FragmentAnimatedTitle
        title="Disc<span_class='special-font'>o</span>ver the world's <br /> largest shared <span_class='special-font'>a</span>dventure"
      />
      <div class="about-subtext">
        <p>The game of Games begins-your life, now an epic MMORPG</p>
        <p>Zentry unites every player from countless games and platforms</p>
      </div>
    </div>

    <div id="clip" class="relative h-dvh">
      <div class="mask-clip-path about-image">
        <img
          alt="zentry"
          src="~/assets/img/about.webp"
          class="absolute top-0 left-0 size-full object-cover"
        />
      </div>
    </div>
  </section>
</template>
