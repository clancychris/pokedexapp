<template>
  <div class="fex flex-col space-y-6">
    <h1 class="text-6xl text-grey-900 font-semibold">
      {{ pokemonDetails?.name }}
    </h1>
    <div>
      <img :src="image" alt="pokemonDetails?.name" />
      <div class="flex items-center space-x-4">
        <span>Primary Type:</span>
        <span>{{ pokemonDetails?.type1 }}</span>
      </div>
      <div class="flex items-center space-x-4" v-if="pokemonDetails?.type2">
        <span>Secondary Type:</span>
        <span>{{ pokemonDetails?.type2 }}</span>
      </div>
    </div>
    <div>
      <div class="flex items-center space-x-4">
        <span>Weight:</span>
        <span>{{ pokemonDetails?.stats?.weight_kg }}</span>
      </div>

      <div class="flex items-center space-x-4">
        <span>Height:</span>
        <span>{{ pokemonDetails?.stats?.height_m }}</span>
      </div>
    </div>
  </div>
</template>

<script setup>
import { useRoute } from "vue-router";
// import pokemons from "@/assets/sampledataset.json";
import { onMounted, ref } from "vue";
import client from "@/assets/apiclient.js";

import axios from "axios";

const route = useRoute();

const pokemonDetails = ref({});

const image = ref("");

onMounted(() => {
  // pokemonDetails.value = pokemons.filter(
  //   (item) => item.name.toLowerCase() == route.params.name.toLowerCase()
  // )[0];

  client
    .get(`pokemon/${route.params.name}`)
    .then((res) => {
      console.log("response received", res.data);
      pokemonDetails.value = res.data;

      axios
        .get(
          `https://pokeapi.co/api/v2/pokemon/${pokemonDetails.value.name.toLowerCase()}`
        )
        .then((data) => {
          image.value =
            data.data.sprites.other["official-artwork"].front_default;
        });
    })
    .catch((errors) => {
      console.log("error", errors);
    });
});
</script>
