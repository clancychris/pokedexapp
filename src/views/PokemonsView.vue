<template>
  <div>
    <PokemonList />
  </div>
</template>

<script setup>
import { defineAsyncComponent } from "vue";

const PokemonList = defineAsyncComponent(() =>
  import("@/components/PokemonList.vue")
);
</script>

<style lang="scss" scoped></style>
