<script setup lang="ts">
import EventCard from "~/components/EventCard.vue";
import { EventData } from "~/utils/types/index";

const events = ref<EventData[]>([]);

const { data, pending, error } = await useFetch<{ data: EventData[] }>(
  "http://localhost:3001/events"
);

events.value = data.value ? data.value.data : [];
</script>

<template>
  <h1>Welcome to 3cket Home Page</h1>

  <div v-if="pending" class="loading">Loading...</div>

  <div v-if="error" class="error">
    Failed to fetch events. Please try again later.
  </div>

  <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
    <EventCard v-for="event in events" :key="event.id" :event="event" />
  </div>
</template>
