<script setup>
import { RouterLink, RouterView } from "vue-router";
</script>

<template>
  <RouterView />
</template>

<style>
@import "@/assets/base.css";

#app {
  max-width: 1280px;
  margin: 0 auto;
  padding: 2rem;
  width: 100%;
  font-weight: normal;
}

@media (min-width: 1024px) {
  body {
    display: flex;
    place-items: center;
  }
}
</style>
