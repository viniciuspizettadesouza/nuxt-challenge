<script setup lang="ts">
import { EventData } from "~/utils/types/index";

const route = useRoute();
const event = ref<EventData>();

function formatDate(datetime: string) {
  const options = {
    year: "numeric",
    month: "long",
    day: "numeric",
    hour: "2-digit",
    minute: "2-digit",
  };
  return new Date(datetime).toLocaleDateString(undefined, options);
}

const { data, pending, error } = await useFetch<{ data: EventData }>(
  `http://localhost:3001/events/${route.params.slug}`,
);

if (data.value) {
  event.value = data.value.data;
}
</script>

<template>
  <div v-if="pending" class="loading">Loading...</div>

  <div v-if="error" class="error flex flex-col items-center">
    <h2>Evento não encontrado, deseja voltar para a página principal?</h2>
    <button
      @click="navigateTo('/')"
      class="mt-4 w-1/3 rounded bg-blue-500 px-4 py-2 text-white"
    >
      Voltar
    </button>
  </div>

  <div v-if="event" class="min-h-screen px-4 py-8">
    <section class="mb-4 flex items-center justify-between">
      <h1 class="text-3xl font-semibold">{{ event.name }}</h1>
      <button class="mt-2 w-32 rounded bg-blue-500 p-2 text-white">
        Buy Tickets
        <Icon name="mdi:chevron-right" class="" />
      </button>
    </section>

    <div
      class="h-64 bg-cover bg-center md:h-96"
      :style="{
        backgroundImage: `url('${event.theme.background_image.url}')`,
      }"
    ></div>

    <div class="rounded-lg bg-white p-6 shadow-md">
      <p class="mb-3">
        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Quisque
        vehicula sapien euismod tempor tristique. Fusce in ultrices lorem. Morbi
        egestas venenatis dolor, nec faucibus ante iaculis hendrerit.
        Suspendisse malesuada finibus laoreet. Integer orci sem, egestas sed
        blandit at, mollis et nibh. Integer et mattis lectus. Maecenas in ornare
        lorem. Praesent fermentum pellentesque tortor, nec faucibus lectus
        semper quis. Mauris mi dui, elementum nec metus quis, semper blandit
        orci. Sed facilisis eleifend ex, id hendrerit velit maximus a.
      </p>

      <div class="grid grid-cols-2 gap-4">
        <div>
          <img
            v-if="event.theme.background_image.url"
            :src="event.theme.background_image.url"
            alt="Event Image"
            class="w-full rounded-lg"
          />
          <div v-else class="h-40 w-full rounded-lg bg-gray-300"></div>
        </div>

        <section>
          <p><strong>Category:</strong> {{ event.category }}</p>
          <p><strong>Status:</strong> {{ event.status }}</p>
          <p>
            <strong>Location:</strong> {{ event.location.name }},
            {{ event.location.country }}
          </p>
          <p><strong>Starts At:</strong> {{ formatDate(event.starts_at) }}</p>
          <p><strong>Ends At:</strong> {{ formatDate(event.ends_at) }}</p>
          <p>
            <strong>Price Range:</strong>
            {{ event.price_range.minimum.amount }} -
            {{ event.price_range.maximum.amount }}
            {{ event.price_range.minimum.currency }}
          </p>

          <button class="mt-2 w-32 rounded bg-blue-500 p-2 text-white">
            Buy Tickets
            <Icon name="mdi:chevron-right" class="" />
          </button>
        </section>
      </div>
    </div>
  </div>
</template>
