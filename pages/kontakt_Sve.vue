<template>

  <NuxtLayout :name="layout">
    <figure
      class="h-[300px] min-h-[300px] respons w-[250px] bg-[#919995] clip4 absolute left-0 top-20 sm:translate-y-20 z-0"
    ></figure>
    <figure
      class="h-[300px] min-h-[300px] respons w-[250px] bg-[#2c2c2c] clip2 absolute right-0 bottom-0 sm:translate-y-10"
    ></figure>
    <main class="sm:flex sm:flex-row flex flex-col sm:items-start items-center flex-wrap relative sm:mt-28 ">
      <section class="w-[95vw] sm:w-[55%] h-[600px] relative z-50 sm:mb-0 mb-40">
        <div
          class="absolute sm:w-[500px] w-full h-[733px] bg-[#256c2b] kontakt-faner-tablet sm:left-40 container-respons rounded-b-2xl shadow-2xl shadow-[#00000050]"
        >
          <div
            class="flex flex-col flex-wrap text-white h-full items-center justify-evenly gap-10 -translate-y-4"
          >
            <h1 class="">{{ data?.title }}</h1>
            <div class="flex flex-col items-center gap-5">
              <div class="flex items-center justify-center gap-7 hover:underline">
                <img
                  src="https://i.ibb.co/9nXk0H1/icons8-phone-50.png"
                  alt=""
                  class="h-[55px]"
                />
                <a href="tel:+45 88 27 63 33" class="min-w-fit">
                  <p class="min-w-full">{{ data?.title2 }} <br  />{{ data?.title3 }}</p></a
                >
              </div>
              <div class="w-full flex items-center gap-7 hover:underline">
                <img
                  src="https://i.ibb.co/z54gmW8/icons8-email-64-2.png"
                  alt=""
                  class="h-[49px]"
                />
                <a href="mailto:mail@ikr.dk" class="min-w-fit">
                  <p class="min-w-full">{{ data?.title4 }} <br />{{ data?.title5 }}</p></a
                >
              </div>
            </div>
            <p class="w-[80%] text-center">
              <PortableText v-if="data?.text1?.[0]" :value="data.text1[0]" :components="components" />
            </p>
          </div>
        </div>
      </section>
      <section class="z-50 sm:w-fit w-[95vw] ">
        <Form
          :validation-schema="schema"
          @submit="onSubmit"
          class="bg-[#256c2b] kontakt-faner-tablet w-full p-8 rounded-b-3xl sm:rounded-t-none rounded-t-3xl shadow-2xl shadow-[#00000050]"
        >
          <label for="navn" class="block mb-4 text-white"
            >{{ data?.title6 }}
            <Field
              name="name"
              type="text"
              class="w-full px-3 py-2 border rounded text-black"
            />
            <ErrorMessage name="name" class="text-red-300 text-sm" />
          </label>

          <label for="telefon" class="block mb-4 text-white"
            >{{ data?.title7 }}
            <Field
              name="phone"
              type="tel"
              class="w-full px-3 py-2 border rounded text-black"
            />
            <ErrorMessage name="phone" class="text-red-300 text-sm" />
          </label>

          <label for="email" class="block mb-4 text-white"
            >{{ data?.title8 }}
            <Field
              type="email"
              name="email"
              class="w-full px-3 py-2 border rounded text-black"
            />
            <ErrorMessage name="email" class="text-red-300 text-sm" />
          </label>

          <label for="virksomhed" class="block mb-4 text-white"
            >{{ data?.title9 }}
            <Field
              type="text"
              name="virksomhed"
              class="w-full px-3 py-2 border rounded text-black"
            />
            <ErrorMessage name="virksomhed" class="text-red-300 text-sm" />
          </label>

          <label for="besked" class="block mb-4 text-white"
            >{{ data?.title10 }}
            <Field
              as="textarea"
              name="text"
              rows="4"
              class="w-full px-3 py-2 border rounded text-black"
            ></Field>
          </label>

          <button
            type="submit"
            :disabled="sending"
            :class="messageSent ? 'bg-green-500' : 'bg-[#0a3700]'"
            class="text-white px-4 py-2 rounded hover:scale-110 transition-all font-semibold disabled:opacity-60 disabled:scale-100"
          >
            {{ messageSent ? 'Skickat!' : sending ? 'Skickar...' : 'Skicka' }}
          </button>
          <span v-if="messageSent" class="text-white ml-4">Meddelande skickat! - vi kontaktar dig.</span>
          <span v-if="sendError" class="text-red-300 ml-4">{{ sendError }}</span>
        </Form>
      </section>
    </main>
  </NuxtLayout>
</template>

<script setup>
import { ref } from "vue";
import { Field, Form, ErrorMessage } from "vee-validate";
import * as yup from "yup";
import { PortableText } from "@portabletext/vue";

const messageSent = ref(false);
const sending = ref(false);
const sendError = ref("");

const schema = yup.object({
  name: yup.string().required(),
  phone: yup.string().required(),
  email: yup.string().email().required(),
  virksomhed: yup.string().required(),
});

async function onSubmit(values) {
  sending.value = true;
  sendError.value = "";
  try {
    await $fetch("/api/send-email", {
      method: "POST",
      body: values,
    });
    messageSent.value = true;
  } catch {
    sendError.value = "Det gick inte att skicka e-post. Försök igen.";
  } finally {
    sending.value = false;
  }
}

const query = groq`*[(_type == "Kontakt") && lang == "Svensk" ][0]`;
const { data } = useSanityQuery(query);

definePageMeta({
  layout: 'svensk-layout'
})

useSeoMeta({
  title: 'Contact IKR today and learn more about your optimization options',
  ogTitle: 'Contact IKR today and learn more about your optimization options',
  description: 'At IKR, were always ready by the phone to assist with clarification on various questions. Contact us today and inquire about your options.',
  ogDescription: 'At IKR, were always ready by the phone to assist with clarification on various questions. Contact us today and inquire about your options.',
  ogImage: 'https://i.ibb.co/JCjnNn8/IKR-Without-Slogan-2400x1800.jpg',
})
</script>

<style scoped>
@media screen and (min-width: 1700px) {
  .container-respons {
    left: 40%;
  }
}

@keyframes slideDown {
  0% {
    opacity: 0.5;
    transform: translateY(-100%);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}

main {
  opacity: 0;
  animation: slideDown 1.5s ease-out forwards;
}

.clip2 {
  clip-path: polygon(0 51%, 100% 0, 100% 51%, 0% 100%);
}

.clip4 {
  clip-path: polygon(0 35%, 63% 0, 63% 65%, 0 100%);
}
</style>
