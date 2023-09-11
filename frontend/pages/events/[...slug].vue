<script setup lang="ts">
import { EventData } from "~/utils/types/index";

const route = useRoute();
const event = ref<EventData>();

const { data, pending, error } = await useFetch<{ data: EventData }>(
  `http://localhost:3001/events/${route.params.slug}`
);

if (data.value) {
  event.value = data.value.data;
}

function navigateHome() {
  navigateTo("/");
}
</script>

<template>
  <div v-if="pending" class="loading">Loading...</div>

  <div v-if="error" class="error flex flex-col items-center">
    <h2>Evento não encontrado, deseja voltar para a página principal?</h2>
    <button
      @click="navigateHome"
      class="bg-blue-500 text-white px-4 py-2 rounded mt-4 w-1/3"
    >
      Voltar
    </button>
  </div>

  <div v-if="event" class="bg-gray-100 min-h-screen py-8">
    <div class="container mx-auto px-4">
      <section class="flex justify-between items-center mb-4">
        <h1 class="text-3xl font-semibold">{{ event.name }}</h1>
        <button class="bg-blue-500 text-white px-4 py-2 rounded mt-2 w-32">
          Comprar
          <Icon name="mdi:chevron-right" class="" />
        </button>
      </section>

      <div
        class="bg-cover bg-center h-64 md:h-96"
        :style="{
          backgroundImage: `url('${event.theme.background_image.url}')`,
        }"
      ></div>

      <div class="bg-white shadow-md rounded-lg p-6">
        <p class="mb-3">
          Lorem ipsum dolor sit amet, consectetur adipiscing elit. Quisque
          vehicula sapien euismod tempor tristique. Fusce in ultrices lorem.
          Morbi egestas venenatis dolor, nec faucibus ante iaculis hendrerit.
          Suspendisse malesuada finibus laoreet. Integer orci sem, egestas sed
          blandit at, mollis et nibh. Integer et mattis lectus. Maecenas in
          ornare lorem. Praesent fermentum pellentesque tortor, nec faucibus
          lectus semper quis. Mauris mi dui, elementum nec metus quis, semper
          blandit orci. Sed facilisis eleifend ex, id hendrerit velit maximus a.
        </p>

        <div class="grid grid-cols-2 gap-4">
          <div>
            <img
              v-if="event.theme.background_image.url"
              :src="event.theme.background_image.url"
              alt="Event Image"
              class="w-full rounded-lg"
            />
            <div v-else class="w-full h-40 bg-gray-300 rounded-lg"></div>
          </div>

          <section>
            <p><strong>Category:</strong> {{ event.category }}</p>
            <p><strong>Status:</strong> {{ event.status }}</p>
            <p>
              <strong>Location:</strong> {{ event.location.name }},
              {{ event.location.country }}
            </p>
            <p><strong>Starts At:</strong> {{ event.starts_at }}</p>
            <p><strong>Ends At:</strong> {{ event.ends_at }}</p>
            <p>
              <strong>Price Range:</strong>
              {{ event.price_range.minimum.amount }} -
              {{ event.price_range.maximum.amount }}
              {{ event.price_range.minimum.currency }}
            </p>

            <button class="bg-blue-500 text-white px-4 py-2 rounded mt-2 w-32">
              Comprar
              <Icon name="mdi:chevron-right" class="" />
            </button>
          </section>
        </div>
      </div>
    </div>
  </div>
</template>
