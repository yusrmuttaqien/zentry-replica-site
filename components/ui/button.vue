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
    <p class="font-general relative"><slot name="text" /></p>
    <slot name="icon-right" />
  </button>
</template>
