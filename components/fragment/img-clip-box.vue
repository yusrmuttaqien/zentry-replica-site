<script setup lang="ts">
const props = defineProps<{
  src: string;
}>();
</script>

<template>
  <div>
    <img :src="props.src" :alt="props.src" />
  </div>
</template>
