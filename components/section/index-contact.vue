<script setup lang="ts">
import IContact1 from "~/assets/img/contact-1.webp";
import IContact2 from "~/assets/img/contact-2.webp";
import ISWMPartial from "~/assets/img/swordman-partial.webp";
import ISWM from "~/assets/img/swordman.webp";
</script>

<template>
  <section id="contact" class="my-20 min-h-96 px-10">
    <div
      class="relative rounded-lg bg-black py-24 text-blue-50 sm:overflow-hidden"
    >
      <div
        class="absolute top-0 -left-20 hidden h-full w-72 overflow-hidden sm:block lg:left-20
          lg:w-96"
      >
        <FragmentImgClipBox :src="IContact1" class="contact-clip-path-1" />
        <FragmentImgClipBox
          :src="IContact2"
          class="contact-clip-path-2 translate-y-60 lg:translate-y-40"
        />
      </div>

      <div
        class="absolute -top-40 left-20 w-60 sm:top-1/2 md:right-10 md:left-auto lg:top-20
          lg:w-80"
      >
        <FragmentImgClipBox :src="ISWMPartial" class="absolute md:scale-125" />
        <FragmentImgClipBox
          :src="ISWM"
          class="sword-man-clip-path md:scale-125"
        />
      </div>

      <div class="relative z-20 flex flex-col items-center text-center">
        <p class="font-general text-[10px] uppercase">Join Zentry</p>

        <p
          class="font-zentry mt-10 w-full text-5xl leading-[0.9] md:text-[6rem]"
        >
          Let's b<span class="special-font">u</span>ild the new era of <br />
          g<span class="special-font">a</span>ming t<span class="special-font"
            >o</span
          >gether
        </p>

        <UiButton class="mt-10"><template #text>Contact us</template></UiButton>
      </div>
    </div>
  </section>
</template>
