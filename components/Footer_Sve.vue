<template>
  <footer
    class="block min-h-[200px] sm:mt-40 mt-28 bg-[#256c2b] pt-5 text-white"
  >
    <div
      class="flex-col gap-10 sm:gap-0 sm:flex-row flex w-full justify-around items-end"
    >
      <NuxtLink to="/index_Eng"
        ><img
          src="https://i.ibb.co/yqJCFL2/IKR-Inverted-Color-800x600-2-1.png"
          class="h-[170px] tablet-img-footer"
      /></NuxtLink>

      <div class="flex flex-col gap-2 sm:w-fit w-full">
        <div
          class="flex gap-2 flex-col items-center sm:items-start justify-center sm:text-start"
        >
          <NuxtLink
            class="text-[18px] hover:underline hover:underline-offset-4"
            to="/index_Sve"
            >HEM</NuxtLink
          >
          <NuxtLink
            class="text-[18px] hover:underline hover:underline-offset-4"
            to="samarbejde_Sve"
            >SAMARBETE
          </NuxtLink>
          <NuxtLink
            class="text-[18px] hover:underline hover:underline-offset-4"
            to="ydelser_Sve"
            >TJÄNSTER
          </NuxtLink>
          <NuxtLink
            class="text-[18px] hover:underline hover:underline-offset-4"
            to="vi-er_Sve"
            >VI ÄR
          </NuxtLink>
          <NuxtLink
            class="text-[18px] hover:underline hover:underline-offset-4"
            to="faq_Sve"
            >FAQ
          </NuxtLink>
          <NuxtLink
            class="text-[18px] hover:underline hover:underline-offset-4"
            to="kontakt_Sve"
            >KONTAKT
          </NuxtLink>
          <NuxtLink
            class="text-[18px] hover:underline hover:underline-offset-4"
            to="ikrlegal"
            >IKR legal
          </NuxtLink>
        </div>
      </div>
      <div
        class="flex flex-col w-fit items-center sm:text-left text-center sm:m-0 m-auto"
      >
        <div class="flex flex-col">
          <p class="mt-4 text-[18px] max-w-[128px]">
            Gustav III:s Boulevard,<br />
            169 73 Solna
          </p>
        </div>
        <div class="flex flex-col mt-1">
          <a href="tel:+46 850 780 615"
            ><p
              class="mt-4 text-[18px] hover:underline hover:underline-offset-4"
            >
            +46 850 780 615
            </p></a
          >
          <a href="mailto:mail@ikr.dk"
            ><p
              class="mt-2 text-[18px] hover:underline hover:underline-offset-4"
            >
              mail@ikr.dk
            </p></a
          >
        </div>
        <div class="flex flex-col">
          <p class="mt-4 text-[18px]">CVR - 27185045</p>
        </div>
        <a
          target="_blank"
          rel="noopener noreferrer"
          href="https://dk.linkedin.com/company/ikr-a-s"
          class="h-fit w-fit"
        >
          <img
            src="https://i.ibb.co/XpCTQVq/Linked-In-icon-svg-1.png"
            class="w-10 mt-5"
          />
        </a>
      </div>
      <div class="flex flex-col gap-10 items-center sm:w-[280px] w-full">
        <NuxtLink to="kontakt_Eng"
          ><button
            class="text-white hover:scale-110 transition-all bg-[#2c2c2c] h-[60px] w-[350px] rounded-sm tablet-knap-footer"
          >
            <h5>KONTAKTA OSS</h5>
          </button></NuxtLink
        >
        <a
          href="https://www.bisnode.dk/om-bisnode/hvad-vi-gor/live-rating-logo-eng/"
          target="_blank"
          class="no-underline"
        >
          <img
            class="h-[94px]"
            src="https://merit.soliditet.dk/merit/imageGenerator/display?lang=EN&country=DK&cId=hKnZW3dMD8Pk99j1fyB7CA%3D%3D&cUid=cnJngSjDhuE%3D&imgType=img_273_73_px"
            oncontextmenu="return false"
            title="Our company is credit worthy according to Bisnode's credit assessment system that is based on a number of decision rules. This credit rating is updated on a daily basis, and always shows the current rating and date."
            alt="Our company is credit worthy according to Bisnode's credit assessment system that is based on a number of decision rules. This credit rating is updated on a daily basis, and always shows the current rating and date."
            id="img_273_73_px"
          />
        </a>
      </div>
    </div>
    <div class="h-10"></div>
    <p class="flex justify-center text-[15px]">Copyright © 2024 IKR A/S | All rights reserved</p>
  </footer>
</template>

<script>
export default {};
</script>

<style>
body > div > main > footer {
  display: none !important;
}
</style>