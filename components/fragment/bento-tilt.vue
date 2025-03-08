<script setup lang="ts">
import gsap from "gsap";

const wrapper = ref<HTMLDivElement | null>(null);

function handleMouseMove(e: MouseEvent) {
  if (!wrapper.value) return;
  const { left, top, width, height } = wrapper.value.getBoundingClientRect();
  const relativeX = (e.clientX - left) / width;
  const relativeY = (e.clientY - top) / height;
  const tiltX = (relativeY - 0.5) * 5;
  const tiltY = (relativeX - 0.5) * -5;

  gsap.to(wrapper.value, {
    rotateX: `${tiltX}deg`,
    rotateY: `${tiltY}deg`,
    overwrite: "auto",
    scale: 0.98,
    duration: 0.8,
    ease: "power3",
  });
}
function handleMouseLeave() {
  gsap.to(wrapper.value, {
    overwrite: "auto",
    rotateX: `0deg`,
    rotateY: `0deg`,
    scale: 1,
    duration: 0.8,
    ease: "power3",
  });
}

onMounted(() => {
  gsap.set(wrapper.value, { transformPerspective: "700px" });
});
</script>

<template>
  <div
    ref="wrapper"
    @mousemove="handleMouseMove"
    @mouseleave="handleMouseLeave"
  >
    <slot />
  </div>
</template>
