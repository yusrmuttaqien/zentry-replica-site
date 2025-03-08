<script setup lang="ts">
import gsap from "gsap";
const frame = ref<HTMLImageElement | null>(null);

function handleMouseLeave() {
  gsap.to(frame.value, {
    rotateX: `0deg`,
    rotateY: `0deg`,
    duration: 0.3,
    ease: "power3",
  });
}
function handleMouseMove(e: MouseEvent) {
  const { clientX, clientY } = e;
  const element = frame.value;

  if (!element) return;
  const { left, top, width, height } = element.getBoundingClientRect();
  const x = clientX - left;
  const y = clientY - top;
  const centerX = width / 2;
  const centerY = height / 2;
  const rotateX = ((y - centerY) / centerY) * -10;
  const rotateY = ((x - centerX) / centerX) * 10;

  gsap.to(element, {
    rotateX: `${rotateX}deg`,
    rotateY: `${rotateY}deg`,
    overwrite: "auto",
    duration: 0.3,
    ease: "power3",
  });
}

onMounted(() => {
  gsap.set(frame.value, { transformPerspective: "700px" });
});
</script>

<template>
  <section id="story" class="min-h-dvh bg-black text-blue-50">
    <div class="flex size-full flex-col items-center py-10 pb-24">
      <p class="font-general text-sm uppercase md:text-[10px]">
        The multiversal IP world
      </p>

      <div class="relative size-full">
        <FragmentAnimatedTitle
          class="pointer-events-none relative z-10 mt-5 mix-blend-difference"
          title="The st<span_class='special-font'>o</span>ry of a hidden real<span_class='special-font'>m</span>"
        />

        <div class="story-img-container">
          <div class="story-img-mask">
            <div class="story-img-content">
              <img
                ref="frame"
                alt="enterance"
                class="object-contain"
                @mouseup="handleMouseLeave"
                @mousemove="handleMouseMove"
                @mouseleave="handleMouseLeave"
                @mouseenter="handleMouseLeave"
                src="~assets/img/entrance.webp"
              />
            </div>
          </div>

          <FragmentStoryImgRound />
        </div>
      </div>

      <div
        class="relative z-10 -mt-80 flex w-full justify-center md:me-44 md:-mt-64
          md:justify-end"
      >
        <div class="flex h-full w-max flex-col items-center md:items-start">
          <p
            class="font-circular-web mt-3 max-w-sm text-center text-violet-50 md:text-start"
          >
            Where realms converge, lies Zentry and the boundless pillar.
            Discover its secrets and shape your fate amidst infinite
            opportunities.
          </p>
          <UiButton id="realm-button" class="mt-5">
            <template #text>Discover prolouge</template>
          </UiButton>
        </div>
      </div>
    </div>
  </section>
</template>
