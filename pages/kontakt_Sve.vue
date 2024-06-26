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
            <h1 class="">{{ data.title }}</h1>
            <div class="flex flex-col items-center gap-5">
              <div class="flex items-center justify-center gap-7 hover:underline">
                <img
                  src="https://i.ibb.co/9nXk0H1/icons8-phone-50.png"
                  alt=""
                  class="h-[55px]"
                />
                <a href="tel:+45 88 27 63 33" class="min-w-fit">
                  <p class="min-w-full">{{ data.title2 }} <br  />{{ data.title3 }}</p></a
                >
              </div>
              <div class="w-full flex items-center gap-7 hover:underline">
                <img
                  src="https://i.ibb.co/z54gmW8/icons8-email-64-2.png"
                  alt=""
                  class="h-[49px]"
                />
                <a href="mailto:mail@ikr.dk" class="min-w-fit">
                  <p class="min-w-full">{{ data.title4 }} <br />{{ data.title5 }}</p></a
                >
              </div>
            </div>
            <p class="w-[80%] text-center">
              <PortableText :value="data.text1[0]" :components="components" />
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
            >{{ data.title6 }}
            <Field
              name="name"
              type="name"
              class="w-full px-3 py-2 border rounded text-black"
            />
            <ErrorMessage name="name" />
          </label>
  
          <label for="telefon" class="block mb-4 text-white"
            >{{ data.title7 }}
            <input
              v-model="telefon"
              type="phone"
              id="telefon"
              name="phone"
              class="w-full px-3 py-2 border rounded text-black"
              required
            />
          </label>
  
          <label for="email" class="block mb-4 text-white"
            >{{ data.title8 }}
            <Field
              type="email"
              name="email"
              class="w-full px-3 py-2 border rounded text-black"
            />
          </label>
  
          <label for="virksomhed" class="block mb-4 text-white"
            >{{ data.title9 }} 
            <Field
              type="virksomhed "
              name="virksomhed"
              class="w-full px-3 py-2 border rounded text-black"
            />
          </label>
  
          <label for="besked" class="block mb-4 text-white"
            >{{ data.title10 }}
            <Field
              as="textarea"
              name="text"
              v-model="text"
              rows="4"
              class="w-full px-3 py-2 border rounded text-black"
            ></Field>
          </label>
  
          <button
    :class="messageSent ? 'bg-green-500' : 'bg-[#0a3700]'"
    class="text-white px-4 py-2 rounded hover:scale-110 transition-all font-semibold"
    @click="sendMessage"
  >
    {{ messageSent ? 'Sent!' : 'Send' }}
  </button>
          <span v-if="messageSent" class="text-white ml-4"
            >Message sent! - we will contact you.</span
          >
        </Form>
  
        <div v-if="isNotificationVisible" class="notification-modal grid">
          <p>{{ notificationMessage }}</p>
          <button
            class="bg-SubColor2 p-2 text-lg rounded-lg mt-4 m-auto text-gray-100"
            @click="closeForm"
          >
            X
          </button>
        </div>
      </section>
    </main>
  </NuxtLayout>
</template>

<script setup>
import { ref } from "vue";
import { Field, Form, ErrorMessage } from "vee-validate";
import * as yup from "yup";
const messageSent = ref(false); 

async function onSubmit(value) {
  const schema = yup.object({
    name: yup.string().required(),
    phone: yup.string().required(),
    email: yup.string().email(),
    virksomhed: yup.string().required(),
  });
  // Data der skal sendes til backend
  const formData = {
    name: value.name,
    phone: value.phone,
    email: value.email,
    virksomhed: value.virksomhed,
    text: value.text,
  };
  try {
    const response = await fetch("https://ikrmail.webtify.dk/send-email", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify(formData),
    });
    const data = await response.json();
    console.log(data);
    if (response.ok) {
      notificationMessage.value = "E-mail sendt!";
      isNotificationVisible.value = true;
    } else {
      notificationMessage.value = "Fejl ved afsendelse af e-mail.";
      isNotificationVisible.value = true;
    }
  } catch (error) {
    console.error("There was an error sending the e-mail:", error);
  }
}

const isNotificationVisible = ref(false);
const notificationMessage = ref("");
function sendMessage() {
  messageSent.value = true; // This will change the button's state immediately when clicked
  onSubmit(); // Call your existing submit function
}
const query = groq`*[(_type == "Kontakt") && lang == "Svensk" ][0]`;

const sanity = useSanity();
const { data } = useSanityQuery(query);
import { PortableText } from "@portabletext/vue";
console.log(data);

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