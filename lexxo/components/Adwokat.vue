<script setup>
import { ref } from 'vue';
import { usePrismic } from '@prismicio/vue';

const { client } = usePrismic();

const firstName = ref('');
const lastName = ref('');

const { data: posts } = await useAsyncData("adwokat", async () => {
  const response = await client.getAllByType("adwokat");

  if (response.results.length > 0) {
    const adwokat = response.results[0];
    firstName.value = adwokat.data.first_name;
    lastName.value = adwokat.data.last_name;
    console.log(firstName.value, lastName.value); // Dodaj tę linię
  }

  return response.results;
});
</script>

<template>
    <h1>{{ firstName }} {{ lastName }}</h1>
  </template>