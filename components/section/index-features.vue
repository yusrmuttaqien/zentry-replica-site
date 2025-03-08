<script setup lang="ts">
import VFeature1 from "~/assets/videos/feature-1.mp4";
import VFeature2 from "~/assets/videos/feature-2.mp4";
import VFeature3 from "~/assets/videos/feature-3.mp4";
import VFeature4 from "~/assets/videos/feature-4.mp4";
import VFeature5 from "~/assets/videos/feature-5.mp4";
</script>

<template>
  <section class="bg-black pb-52 text-blue-50">
    <div class="container mx-auto px-3 md:px-10">
      <div class="px-5 py-32">
        <p class="font-circular-web text-lg">Into the Metagame Layer</p>
        <p class="font-circular-web max-w-md text-lg text-blue-50/50">
          Immerse yourself in a rich and ever-expanding universe where a vibrant
          array of products converge into an interconnected overlay experience
          on your world.
        </p>
      </div>
      <FragmentBentoTilt
        class="border-hsla relative mb-7 h-96 w-full overflow-hidden rounded-md md:h-[65vh]"
      >
        <FragmentBentoCard
          :src="VFeature1"
          description="A cross-platform metagame app, turning your activities across Web2 and Web3 games into a rewarding adventure."
        >
          <template #title>radia<span class="special-font">n</span>t</template>
        </FragmentBentoCard>
      </FragmentBentoTilt>

      <div class="grid h-[135vh] grid-cols-2 grid-rows-3 gap-7">
        <FragmentBentoTilt
          class="bento-tilt-1 row-span-1 md:col-span-1 md:row-span-2"
        >
          <FragmentBentoCard
            :src="VFeature2"
            description="An anime and gaming-inspired NFT collection - the IP primed for expansion."
          >
            <template #title>zig<span class="special-font">m</span>a</template>
          </FragmentBentoCard>
        </FragmentBentoTilt>
        <FragmentBentoTilt
          class="bento-tilt-1 row-span-1 ms-32 md:col-span-1 md:ms-0"
        >
          <FragmentBentoCard
            :src="VFeature3"
            description="A gamified social hub, adding a new dimension of play to social interaction for Web3 communities."
          >
            <template #title>n<span class="special-font">e</span>xus</template>
          </FragmentBentoCard>
        </FragmentBentoTilt>
        <FragmentBentoTilt class="bento-tilt-1 me-14 md:col-span-1 md:me-0">
          <FragmentBentoCard
            :src="VFeature4"
            description="A cross-world AI Agent - elevating your gameplay to be more fun and productive."
          >
            <template #title>az<span class="special-font">u</span>l</template>
          </FragmentBentoCard>
        </FragmentBentoTilt>

        <FragmentBentoTilt class="bento-tilt-2">
          <div
            class="flex size-full flex-col justify-between bg-violet-300 p-5"
          >
            <h1 class="bento-title max-w-64 text-black">
              M<span class="special-font">0</span>re co<span
                class="special-font"
                >m</span
              >ing s<span class="special-font">o</span>on!
            </h1>
            <IconArrowRight
              class="-m-5 -rotate-45 self-end text-[10rem] text-black"
            />
          </div>
        </FragmentBentoTilt>

        <FragmentBentoTilt class="bento-tilt-2">
          <video
            loop
            muted
            autoplay
            :src="VFeature5"
            class="size-full object-cover object-center"
          ></video>
        </FragmentBentoTilt>
      </div>
    </div>
  </section>
</template>
