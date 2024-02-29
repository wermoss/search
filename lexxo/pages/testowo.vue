<script setup>
import { ref } from 'vue';
import { usePrismic } from '@prismicio/vue';

const { client } = usePrismic();

const firstName = ref('');
const secondName = ref(''); // Zmieniłem nazwę z lastName na secondName

const { data: adwokats } = await useAsyncData("adwokats", async () => {
  const response = await client.getAllByType("adwokat");
  console.log('Response from Prismic:', response);

  if (response.results.length > 0) {
    const adwokat = response.results[0];
    firstName.value = adwokat.data.first_name;
    secondName.value = adwokat.data.second_name; // Zaktualizuj tę linię
    console.log(firstName.value, secondName.value); // Zaktualizuj tę linię
  }

  return response.results;
});
</script>

<template>
    <div v-if="firstName && secondName">
      <h1>{{ firstName }} {{ secondName }}</h1> <!-- Zaktualizuj tę linię -->
    </div>
</template>