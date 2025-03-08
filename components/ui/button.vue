<script setup lang="ts">
import type { ComponentEmits } from "~/types/component";

defineEmits<ComponentEmits>();
</script>

<template>
  <button
    class="group relative flex w-max cursor-pointer items-center gap-2 rounded-full
      bg-violet-50 px-7 py-3 text-black uppercase"
  >
    <slot name="icon-left" />
    <p class="font-general relative overflow-hidden">
      <span
        class="block transition-transform duration-500 group-hover:-translate-y-[150%]
          group-hover:skew-y-12"
      >
        <slot name="text" />
      </span>
      <span
        class="absolute top-0 left-0 block translate-y-[150%] skew-y-12 transition-transform
          duration-500 group-hover:translate-y-0 group-hover:skew-y-0"
      >
        <slot name="text" />
      </span>
    </p>
    <slot name="icon-right" />
  </button>
</template>
