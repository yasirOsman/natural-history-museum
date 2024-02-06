<script setup>
import { RouterView } from 'vue-router'
import Navigation from '@/components/Navigation.vue'
</script>

<template>
  <Navigation />
  <RouterView />
</template>

<style>
body {
  background: rgba(3, 0, 21, 1);
  margin: 0;
}
</style>
