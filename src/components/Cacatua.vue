<template>
  <div id="corralito">
    <img :src="`img/cacatua${type}.png`" :alt="`Cacatua${type}`" height="150" />
  </div>
</template>

<script setup>
import { ref } from "vue";
const type = ref(Math.floor(Math.random() * 6) + 1);
</script>
