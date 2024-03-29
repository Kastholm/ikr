<template>
  <head>
    <title>Questions about optimization & contract management - FAQ</title>
    <meta name="description" content="There are many ways to optimize agreements & contracts - read more about the different possibilities & types of agreements here.">
  </head>
  <NuxtLayout :name="layout">
  <FaqHero_Eng />
  <section class="bar-sections relative z-20">
    <figure
      class="h-[300px] min-h-[300px] respons w-[250px] bg-[#919995] clip4 absolute left-0 top-0 sm:-translate-y-6 translate-y-16 z-0"
    ></figure>
    <figure
      class="h-[300px] min-h-[300px] respons w-[250px] bg-[#2c2c2c] clip2 absolute right-0 bottom-0 sm:translate-y-20 translate-y-40 z-0"
    ></figure>
    <h4 class="mmd-text z-50">FAQ</h4>

    <div class="bar z-20" id="bar1">
      <div
        @click="toggleBar('bar1')"
        class="flex justify-center items-center translate-y-3"
      >
        <h3 class="header">
          ANALYSES<br />
          <span style="font-size: 16px"> ▼ </span>
        </h3>
      </div>
      <div class="content">
        <div class="bar-flex">
          <div
            v-for="(worker, index) in data.analyser"
            :key="index"
            class="baranalyser"
            :id="`bar1.${index}`"
          >
            <h6 class="header" @click="toggleBar(`bar1.${index}`)">
              <strong class="text-[35px]">+</strong> {{ worker.bullettitle1 }}
            </h6>
            <div class="content" @click="toggleBar(`bar1.${index}`)">
              <div class="bar-flex2">
                <p class="bar-lille-text">
                  <PortableText
                    :value="worker.bullettext1"
                    :components="component"
                  />
                </p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="bar z-20" id="bar2">
      <h3 class="header translate-y-3" @click="toggleBar('bar2')">
         SUBCONTRACTORS & CONTRACTS<br />
        <span style="font-size: 16px"> ▼ </span>
      </h3>
      <div class="content">
        <div class="bar-flex">
          <div
            v-for="(worker, index) in data.leverandor"
            :key="index"
            class="baranalyser"
            :id="`bar2.${index}`"
          >
            <h6 class="header" @click="toggleBar(`bar2.${index}`)">
              <strong class="text-[35px]">+</strong> {{ worker.bullettitle2 }}
            </h6>
            <div class="content" @click="toggleBar(`bar2.${index}`)">
              <div class="bar-flex2">
                <p class="bar-lille-text">
                  <PortableText
                    :value="worker.bullettext2"
                    :components="component"
                  />
                </p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="bar z-20" id="bar3">
      <h3 class="header translate-y-3" @click="toggleBar('bar3')">
        INCREASED FINANCIAL FLEXIBILITY<br />
        <span style="font-size: 16px"> ▼ </span>
      </h3>
      <div class="content">
        <div class="bar-flex">
          <div
            v-for="(worker, index) in data.okonomi"
            :key="index"
            class="baranalyser"
            :id="`bar3.${index}`"
          >
            <h6 class="header" @click="toggleBar(`bar3.${index}`)">
              <strong class="text-[35px]">+</strong> {{ worker.bullettitle3 }}
            </h6>
            <div class="content" @click="toggleBar(`bar3.${index}`)">
              <div class="bar-flex2">
                <p class="bar-lille-text">
                  <PortableText
                    :value="worker.bullettext3"
                    :components="component"
                  />
                </p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="bar z-20" id="bar4">
      <h3 class="header translate-y-3" @click="toggleBar('bar4')">
        OPERATIONS & CONTROLLING<br />
        <span style="font-size: 16px"> ▼ </span>
      </h3>
      <div class="content">
        <div class="bar-flex">
          <div
            v-for="(worker, index) in data.drift"
            :key="index"
            class="baranalyser"
            :id="`bar4.${index}`"
          >
            <h6 class="header" @click="toggleBar(`bar4.${index}`)">
              <strong class="text-[35px]">+</strong> {{ worker.bullettitle4 }}
            </h6>
            <div class="content" @click="toggleBar(`bar4.${index}`)">
              <div class="bar-flex2">
                <p class="bar-lille-text">
                  <PortableText
                    :value="worker.bullettext4"
                    :components="component"
                  />
                </p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="bar z-20" id="bar5">
      <h3 class="header translate-y-3" @click="toggleBar('bar5')">
        PROCUREMENT & TENDERING<br />
        <span style="font-size: 16px"> ▼ </span>
      </h3>
      <div class="content">
        <div class="bar-flex">
          <div
            v-for="(worker, index) in data.indkob"
            :key="index"
            class="baranalyser"
            :id="`bar5.${index}`"
          >
            <h6 class="header" @click="toggleBar(`bar5.${index}`)">
              <strong class="text-[35px]">+</strong> {{ worker.bullettitle5 }}
            </h6>
            <div class="content" @click="toggleBar(`bar5.${index}`)">
              <div class="bar-flex2">
                <p class="bar-lille-text">
                  <PortableText
                    :value="worker.bullettext5"
                    :components="component"
                  />
                </p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</NuxtLayout>
</template>



<script setup>
const toggleBar = (barId) => {
  const bar = document.getElementById(barId);
  if (bar) {
    bar.classList.toggle("active");
  } else {
    console.error(`Element with id ${barId} not found.`);
  }
};

const query = groq`*[(_type == "faq") && lang == "Engelsk" ][0]`;

const sanity = useSanity();
const { data } = useSanityQuery(query);
import { PortableText } from "@portabletext/vue";
console.log(data);
definePageMeta({
  layout: 'engelsk-layout'
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

main {
  opacity: 0;
  animation: slideDown 0.7s ease-out forwards;
}

.bar-sections {
  display: flex;
  flex-direction: column;
  gap: 40px;
  margin: 100px 0 100px 0;
  width: 100%;
  align-items: center;
}

@media screen and (max-width: 767px) {
  .bar-sections {
    margin: 50px 0 180px 0;
  }
}

.mmd-text {
  font-size: 80px;
}

@media screen and (max-width: 767px) {
  .mmd-text {
    font-size: 31px;
    max-width: 388px;
    text-align: center;
  }
}

.bar {
  width: 50%;
  height: 80px;
  background-color: #0a3700;
  color: white;
  cursor: pointer;
  transition: height 0.5s ease;
  overflow: hidden;
  border-radius: 10px;
  color: rgb(255, 255, 255);
  line-height: 20px;
}

@media screen and (max-width: 767px) {
  .bar {
    min-width: 95vw;
  }
}

.baranalyser {
  width: 70%;
  height: 45px;
  background-color: #256c2b;
  color: white;
  cursor: pointer;
  transition: height 0.5s ease;
  overflow: hidden;
  border-radius: 10px;
  color: rgb(255, 255, 255);
  line-height: 20px;
}

@media screen and (max-width: 767px) {
  .baranalyser {
    min-width: 90vw;
    height: 65px;
  }
}

@media only screen and (min-width: 768px) and (max-width: 1140px) {
  .baranalyser {
    height: 84px;
  }
}

.header {
  padding: 10px;
  text-align: center;
  font-size: 30px;
}

@media screen and (max-width: 767px) {
  .header {
    font-size: 20px;
  }
}

@media only screen and (min-width: 768px) and (max-width: 1140px) {
  .header {
    line-height: 30px;
  }
}

.content {
  display: none;
  padding: 10px;
  text-align: center;
  height: 100%;
  font-size: 20px;
  margin: auto;
  height: fit-content;
}

.bar-flex {
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  gap: 30px;
  align-items: center;
}

.bar-flex2 {
  display: flex;
  flex-direction: column;
  justify-content: start;
  align-items: center;
  height: 100%;
  margin-top: 50px;
  width: 100%;
}

@media screen and (max-width: 767px) {
  .bar-flex2 {
    margin-top: 10px;
  }
}

.content {
  max-width: 1300px;
}

.bar.active {
  height: auto; /* Adjust the height as needed */
  padding-bottom: 50px;
  width: 80%;
}

.baranalyser.active {
  height: auto;
  overflow: hidden; /* Ensure that content does not overflow when height is set to auto */
  transition: height 0.3s ease; /* Add smooth transition animation */ /* Adjust the height as needed */
}

@media screen and (max-width: 767px) {
  .baranalyser.active {
    height: 520px;
  }
}

@media only screen and (min-width: 768px) and (max-width: 1090px) {
  .baranalyser.active {
    height: 700px;
  }
}

@media only screen and (min-width: 768px) and (max-width: 1140px) {
  .baranalyser.active {
    height: 660px;
  }
}

.baranalyser2.active {
  height: 740px;
}

@media screen and (max-width: 767px) {
  .baranalyser2.active {
    height: 730px;
  }
}

@media only screen and (min-width: 768px) and (max-width: 1140px) {
  .baranalyser2.active {
    height: 840px;
  }
}

.baranalyser3.active {
  height: 390px;
}

@media only screen and (min-width: 768px) and (max-width: 1140px) {
  .baranalyser3.active {
    height: 450px;
  }
}

.baranalyser4.active {
  height: 480px;
}

@media screen and (max-width: 767px) {
  .baranalyser4.active {
    height: 520px;
  }
}

@media only screen and (min-width: 768px) and (max-width: 1140px) {
  .baranalyser4.active {
    height: 630px;
  }
}

.baranalyser5.active {
  height: 460px;
}

@media screen and (max-width: 767px) {
  .baranalyser5.active {
    height: 420px;
  }
}

@media only screen and (min-width: 768px) and (max-width: 1140px) {
  .baranalyser5.active {
    height: 520px;
  }
}

.baranalyser6.active {
  height: 590px;
}

@media screen and (max-width: 767px) {
  .baranalyser6.active {
    height: 625px;
  }
}

@media only screen and (min-width: 768px) and (max-width: 1140px) {
  .baranalyser6.active {
    height: 755px;
  }
}

.baranalyser7.active {
  height: 1200px;
}

@media screen and (max-width: 767px) {
  .baranalyser7.active {
    height: 1230px;
  }
}

@media only screen and (min-width: 768px) and (max-width: 1140px) {
  .baranalyser7.active {
    height: 1520px;
  }
}

.baranalyser8.active {
  height: 1850px;
}

@media screen and (max-width: 767px) {
  .baranalyser8.active {
    height: 1910px;
  }
}

@media only screen and (min-width: 768px) and (max-width: 1140px) {
  .baranalyser8.active {
    height: 2360px;
  }
}

.baranalyser9.active {
  height: 1160px; /* Adjust the height as needed */
}

@media screen and (max-width: 767px) {
  .baranalyser9.active {
    height: 1200px;
  }
}

@media only screen and (min-width: 768px) and (max-width: 1140px) {
  .baranalyser9.active {
    height: 1520px;
  }
}

.baranalyser10.active {
  height: 1120px; /* Adjust the height as needed */
}

@media screen and (max-width: 767px) {
  .baranalyser10.active {
    height: 1250px;
  }
}

@media only screen and (min-width: 768px) and (max-width: 1140px) {
  .baranalyser10.active {
    height: 1520px;
  }
}

.baranalyser11.active {
  height: 2180px; /* Adjust the height as needed */
}

@media screen and (max-width: 767px) {
  .baranalyser11.active {
    height: 2240px;
  }
}

@media only screen and (min-width: 768px) and (max-width: 1140px) {
  .baranalyser11.active {
    height: 2780px;
  }
}

.baranalyser12.active {
  height: 1770px; /* Adjust the height as needed */
}

@media screen and (max-width: 767px) {
  .baranalyser12.active {
    height: 1810px;
  }
}

@media only screen and (min-width: 768px) and (max-width: 1140px) {
  .baranalyser12.active {
    height: 2200px;
  }
}

.baranalyser13.active {
  height: 1950px; /* Adjust the height as needed */
}

@media screen and (max-width: 767px) {
  .baranalyser13.active {
    height: 2000px;
  }
}

@media only screen and (min-width: 768px) and (max-width: 1140px) {
  .baranalyser13.active {
    height: 2440px;
  }
}

.baranalyser14.active {
  height: 2120px; /* Adjust the height as needed */
}

@media screen and (max-width: 767px) {
  .baranalyser14.active {
    height: 2090px;
  }
}

@media only screen and (min-width: 768px) and (max-width: 1140px) {
  .baranalyser14.active {
    height: 2510px;
  }
}

.baranalyser15.active {
  height: 2320px; /* Adjust the height as needed */
}

@media screen and (max-width: 767px) {
  .baranalyser15.active {
    height: 2425px;
  }
}

@media only screen and (min-width: 768px) and (max-width: 1140px) {
  .baranalyser15.active {
    height: 2980px;
  }
}

.baranalyser16.active {
  height: 2250px; /* Adjust the height as needed */
}

@media screen and (max-width: 767px) {
  .baranalyser16.active {
    height: 2240px;
  }
}

@media only screen and (min-width: 768px) and (max-width: 1140px) {
  .baranalyser16.active {
    height: 2780px;
  }
}

.baranalyser17.active {
  height: 1710px; /* Adjust the height as needed */
}

@media screen and (max-width: 767px) {
  .baranalyser17.active {
    height: 1730px;
  }
}

@media only screen and (min-width: 768px) and (max-width: 1140px) {
  .baranalyser17.active {
    height: 2170px;
  }
}

.baranalyser18.active {
  height: 2380px; /* Adjust the height as needed */
}

@media screen and (max-width: 767px) {
  .baranalyser18.active {
    height: 2410px;
  }
}

@media only screen and (min-width: 768px) and (max-width: 1140px) {
  .baranalyser18.active {
    height: 2960px;
  }
}

.baranalyser19.active {
  height: 1360px; /* Adjust the height as needed */
}

@media screen and (max-width: 767px) {
  .baranalyser19.active {
    height: 1510px;
  }
}

@media only screen and (min-width: 768px) and (max-width: 1140px) {
  .baranalyser19.active {
    height: 1790px;
  }
}

.baranalyser20.active {
  height: 2180px; /* Adjust the height as needed */
}

@media screen and (max-width: 767px) {
  .baranalyser20.active {
    height: 2245px;
  }
}

@media only screen and (min-width: 768px) and (max-width: 1140px) {
  .baranalyser20.active {
    height: 2780px;
  }
}

.baranalyser21.active {
  height: 2380px; /* Adjust the height as needed */
}

@media screen and (max-width: 767px) {
  .baranalyser21.active {
    height: 2470px;
  }
}

@media only screen and (min-width: 768px) and (max-width: 1140px) {
  .baranalyser21.active {
    height: 3020px;
  }
}

.baranalyser22.active {
  height: 1840px; /* Adjust the height as needed */
}

@media screen and (max-width: 767px) {
  .baranalyser22.active {
    height: 1810px;
  }
}

@media only screen and (min-width: 768px) and (max-width: 1140px) {
  .baranalyser22.active {
    height: 2240px;
  }
}

.baranalyser23.active {
  height: 1870px; /* Adjust the height as needed */
}

@media screen and (max-width: 767px) {
  .baranalyser23.active {
    height: 1915px;
  }
}

@media only screen and (min-width: 768px) and (max-width: 1140px) {
  .baranalyser23.active {
    height: 2310px;
  }
}

.baranalyser24.active {
  height: 2310px; /* Adjust the height as needed */
}

@media screen and (max-width: 767px) {
  .baranalyser24.active {
    height: 2380px;
  }
}

@media only screen and (min-width: 768px) and (max-width: 1140px) {
  .baranalyser24.active {
    height: 2920px;
  }
}

.baranalyser25.active {
  height: 2310px; /* Adjust the height as needed */
}

.baranalyser26.active {
  height: 2280px; /* Adjust the height as needed */
}

@media screen and (max-width: 767px) {
  .baranalyser26.active {
    height: 2350px;
  }
}

@media only screen and (min-width: 768px) and (max-width: 1140px) {
  .baranalyser26.active {
    height: 2950px;
  }
}

.baranalyser27.active {
  height: 2410px; /* Adjust the height as needed */
}

@media screen and (max-width: 767px) {
  .baranalyser27.active {
    height: 2430px;
  }
}

@media only screen and (min-width: 768px) and (max-width: 1140px) {
  .baranalyser27.active {
    height: 3050px;
  }
}

.baranalyser28.active {
  height: 2510px; /* Adjust the height as needed */
}

@media screen and (max-width: 767px) {
  .baranalyser28.active {
    height: 2470px;
  }
}

@media only screen and (min-width: 768px) and (max-width: 1140px) {
  .baranalyser28.active {
    height: 3020px;
  }
}

.baranalyser29.active {
  height: 2180px; /* Adjust the height as needed */
}

@media screen and (max-width: 767px) {
  .baranalyser29.active {
    height: 2265px;
  }
}

@media only screen and (min-width: 768px) and (max-width: 1140px) {
  .baranalyser29.active {
    height: 2780px;
  }
}

.baranalyser30.active {
  height: 2380px; /* Adjust the height as needed */
}

@media screen and (max-width: 767px) {
  .baranalyser30.active {
    height: 2375px;
  }
}

@media only screen and (min-width: 768px) and (max-width: 1140px) {
  .baranalyser30.active {
    height: 2920px;
  }
}

.baranalyser31.active {
  height: 1940px; /* Adjust the height as needed */
}

@media screen and (max-width: 767px) {
  .baranalyser31.active {
    height: 2105px;
  }
}

@media only screen and (min-width: 768px) and (max-width: 1140px) {
  .baranalyser31.active {
    height: 2580px;
  }
}

.baranalyser32.active {
  height: 2210px; /* Adjust the height as needed */
}

@media screen and (max-width: 767px) {
  .baranalyser32.active {
    height: 2215px;
  }
}

@media only screen and (min-width: 768px) and (max-width: 1140px) {
  .baranalyser32.active {
    height: 2650px;
  }
}

.baranalyser33.active {
  height: 1980px; /* Adjust the height as needed */
}

@media screen and (max-width: 767px) {
  .baranalyser33.active {
    height: 1950px;
  }
}

@media only screen and (min-width: 768px) and (max-width: 1140px) {
  .baranalyser33.active {
    height: 2400px;
  }
}

.bar.active .content {
  display: block;
}

.baranalyser.active .content {
  display: block;
}

.bar-img {
  background-size: contain;
  width: 25%;
  border-radius: 10px;
  height: 300px;
}

.bar-img-3 {
  background-size: contain;
  border-radius: 10px;
  height: 200px;
}

.bar-lille-text {
  text-align: start;
  line-height: 34px;
  width: 90%;
  max-width: 800px;
}

.bar-flex-text {
  display: flex;
  flex-direction: column;
  justify-content: start;
  width: 40%;
  height: 70%;
  text-align: start;
  transform: translatey(-100px);
}

@media screen and (max-width: 767px) {
  .bar-flex-text {
    width: 95%;
    transform: translatey(-130px);
  }
}

@media screen and (max-width: 767px) {
  .bar-lille-text {
    font-size: 14px;
    line-height: 27px;
  }
}
</style>