<template>
  <Suspense>
    <template #default><div>
      <h3>bienvenido pepe</h3>
      <Home />
    </div></template>
    <template #fallback></template>
  </Suspense>

</template>

<script setup>

import Home from "./components/Home.vue";
</script>
<style scoped>

</style>
