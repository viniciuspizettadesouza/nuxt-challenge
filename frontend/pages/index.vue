<script setup lang="ts">
import EventCard from "~/components/EventCard.vue";
import { FetchData } from "~/utils/types/index";

const { data, pending, error } = await useFetch<FetchData>(
  "http://localhost:3001/events"
);

const { value } = data;
</script>

<template>
  <h1>Welcome to 3cket Home Page</h1>

  <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4 ">
    <EventCard v-for="event in value?.data" :key="event.id" :event="event" />
  </div>
</template>
