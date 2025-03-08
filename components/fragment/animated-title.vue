<script setup lang="ts">
import gsap from "gsap";

const props = defineProps<{ title: string }>();
const lines = props.title.split("<br />");
const container = ref<HTMLHeadingElement | null>(null);

function wordH(innerHTML: string) {
  return h("span", { innerHTML });
}

onMounted(() => {
  if (!container.value) return;
  const gsapCtx = gsap.context((self) => {
    const titleTimeline = gsap.timeline({
      scrollTrigger: {
        start: "100 bottom",
        end: "center bottom",
        trigger: container.value,
        toggleActions: "play none none reverse",
      },
    });

    titleTimeline.to(".animated-word", {
      opacity: 1,
      transform: "translate3d(0,0,0) rotateY(0deg) rotateX(0deg)",
      ease: "power2.inOut",
      stagger: 0.02,
    });
  }, container.value);
});
</script>

<template>
  <h3 class="font-zentry animated-title" ref="container">
    <span
      :key="line"
      v-for="line in lines"
      class="flex-center max-w-full flex-wrap gap-2 px-10 md:gap-3"
    >
      <component
        :key="word"
        :v-html="word"
        class="animated-word"
        v-for="word in line.split(' ')"
        :is="wordH(word.replace('_', ' '))"
      />
    </span>
  </h3>
</template>
