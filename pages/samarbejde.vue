<template>
  
  <div v-if="!data || data.length === 0" class="flex justify-center items-center">
    <div class="loader"></div>
  </div>
  <main v-else class="flex flex-col justify-center">
    <SamarbejdeHero />
    <section class="flex flex-col">
      <div
        class="flex flex-wrap w-full article-gap relative mt-20 sm:mt-20 sm:gap-20 gap-10 2xl:gap-40 justify-center"
      >
        <img
          src="https://i.ibb.co/bs8KZ9M/Samarbejde-h-jformat-1.jpg"
          alt=""
          class="sm:max-h-[770px] max-h-[500px] rounded-md z-50 sm:translate-y-5 shadow-2xl"
        />
        <article
          class="sm:w-[45%] w-[90%] flex flex-col flex-wrap gap-5 p-5 rounded-xl translate-y-5"
        >
          <h2>{{ data.title2 }}</h2>

          <ul class="flex flex-col gap-4 min-h-[258px]">
            <li
              v-for="(bulletpoint, index) in data.bulletpoint"
              :key="index"
              class="bulletpoint relative ml-16"
            >
              {{ bulletpoint }}
            </li>
          </ul>
        </article>
      </div>

      <div
        class="flex flex-wrap w-full relative mt-20 sm:mt-36 gap-10 article-gap 2xl:gap-40 justify-center"
      >
        <figure
          class="h-[220px] min-h-[200px] respons w-[200px] bg-[#2c2c2c] clip2 absolute right-0 bottom-0 sm:translate-y-[5px]"
        ></figure>
        <article
          class="sm:w-[40%] w-[85%] flex flex-col gap-5 sm:-translate-y-5"
        >
          <h2 class="">{{ data.title3 }}</h2>
          <ul class="flex flex-col gap-4 min-h-[230px] 2xl:min-h-[190px]">
            <li
              v-for="(bulletpoint, index) in data.bulletpoint2"
              :key="index"
              class="bulletpoint relative ml-16"
            >
              {{ bulletpoint }}
            </li>
          </ul>
          <p class="sm:mt-0 sm:mb-0 mb-10">
            <PortableText
          :value="data.text2[0]"
          :components="components"
        />
          </p>
        </article>
        <img
          src="https://i.ibb.co/cJs7Wtc/samarbejde-billede-1.jpg"
          alt=""
          class="max-h-[400px] rounded-md z-50 shadow-2xl respons-mobi"
        />
      </div>
    </section>

    <SamarbejdeBund />
    <LogoKarrusel
      class="translate-y-20 border-t-[#2c2c2c] border-[0px] border-b-[#2c2c2c]"
    />
    <div></div>
  </main>
</template>

<script setup>
const query = groq`*[(_type == "samarbejde") && lang == "Dansk" ][0]`;

const sanity = useSanity();
const { data } = useSanityQuery(query);
import { PortableText } from "@portabletext/vue";
console.log(data);

useSeoMeta({
  title: 'IKR - jeres samarbejdspartner for optimering af økonomi',
  ogTitle: 'IKR - jeres samarbejdspartner for optimering af økonomi',
  description: 'IKR er jeres faste samarbejdspartner når det gælder optimering af jeres nuværende aftaler - få ekstra råderum i økonomien med i samarbejde hos IKR.',
  ogDescription: 'IKR er jeres faste samarbejdspartner når det gælder optimering af jeres nuværende aftaler - få ekstra råderum i økonomien med i samarbejde hos IKR.',
  ogImage: 'https://i.ibb.co/ZWCZJRk/IKR-Main-Logo-600x450-cropped.jpg',
})
</script>

<style scoped>
@keyframes slideDown {
  0% {
    opacity: 0.9;
    transform: translateY(-20px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}

.clip2 {
  clip-path: polygon(0 51%, 100% 0, 100% 51%, 0% 100%);
}

.clip4 {
  clip-path: polygon(0 35%, 63% 0, 63% 65%, 0 100%);
}

main {
  opacity: 0;
  animation: slideDown 0.7s ease-out forwards;
}

.clip2 {
  clip-path: polygon(0 51%, 100% 0, 100% 51%, 0% 100%);
}

.bulletpoint::before {
  content: "•";
  font-size: 35px;
  transform: translatex(-60px) translatey(-5px);
  position: absolute;
  color: #256c2b;
}

@media screen and (max-width: 767px) {
  .respons-mobil {
    display: none; /*Virker ikke til figur??*/
  }
}
</style>