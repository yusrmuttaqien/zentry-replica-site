<script setup lang="ts">
import { IconDiscord, IconTwitch, IconTwitter } from "#components";

const links = [
  { icon: IconDiscord, href: "www.discord.com" },
  { icon: IconTwitch, href: "www.twitch.com" },
  { icon: IconTwitter, href: "www.x.com" },
];
</script>

<template>
  <footer class="bg-violet-300 py-4 text-black">
    <div
      class="container mx-auto flex flex-col items-center justify-between gap-4 px-4
        md:flex-row"
    >
      <p class="text-center text-sm md:text-left">
        &copy; Nova 2024. All rights reserved
      </p>

      <div class="flex justify-center gap-4 md:justify-start">
        <a
          target="_blank"
          :key="link.href"
          :href="link.href"
          v-for="link in links"
          class="transition-colors hover:text-violet-50"
        >
          <component :is="link.icon" />
        </a>
      </div>

      <a
        href="#privacy-policy"
        class="text-center text-sm hover:underline md:text-right"
        >Privacy policy</a
      >
    </div>
  </footer>
</template>
