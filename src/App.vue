<template>
  <h1>Misión Secreta con Cacatúas</h1>
  <Sheep :sheepMax="20" />

  <Suspense>
    <template #default>
      <MessagesTrello />
    </template>
    <template #fallback>
      <h3>Cargando...</h3>
    </template>
  </Suspense>
</template>

<script setup>
import Sheep from "./components/Sheep.vue";
import MessagesTrello from "./components/MessagesTrello.vue";
</script>
