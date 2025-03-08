<script setup lang="ts">
const props = defineProps<{
  src: string;
  description: string;
}>();
</script>

<template>
  <figure class="relative size-full">
    <video
      loop
      muted
      autoplay
      :src="props.src"
      class="absolute top-0 left-0 size-full object-cover"
    />
    <div
      class="relative z-10 flex size-full flex-col justify-between p-5 text-blue-50"
    >
      <div>
        <h1 class="bento-title"><slot name="title" /></h1>
        <p v-if="props.description" class="mt-3 max-w-64 text-xs md:text-base">
          {{ props.description }}
        </p>
      </div>
    </div>
  </figure>
</template>
