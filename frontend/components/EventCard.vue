<script setup lang="ts">
import { EventData } from "~/utils/types/index";

const props = defineProps({
  event: { type: Object as () => EventData, required: true },
});
</script>

<template>
  <div class="max-w-md rounded overflow-hidden shadow-lg bg-white">
    <img
      :src="event.theme.background_image.url"
      alt="Event Image"
      class="w-full h-32 object-cover"
    />
    <div class="px-6 py-4">
      <div class="font-bold text-xl mb-2 text-gray-700">{{ event.name }}</div>
      <p class="text-gray-700 text-base">{{ event.category }}</p>
      <p class="text-gray-700 text-base">
        Location: {{ event.location.name }}, {{ event.location.country }}
      </p>
      <p class="text-gray-700 text-base">
        Price Range: {{ event.price_range.minimum.amount }} -
        {{ event.price_range.maximum.amount }}
        {{ event.price_range.minimum.currency }}
      </p>
    </div>
  </div>
</template>
~/utils/types
