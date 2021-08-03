<template>
  <button :disabled="checkBusy" @click="handleClick">Agregar una Oveja</button>
  <p>La cuenta es: {{ shepps.length }}.</p>
  <div v-if="checkBusy" id="busy"><h1>El corral está lleno</h1></div>
  <div id="corral">
    <img
      v-for="(sheepNumber, index) in shepps"
      :key="index"
      :src="`img/sheep${sheepNumber}.png`"
      alt="Oveja"
      width="125"
      height="104"
    />
    <div id="trick" />
  </div>
</template>

<script setup>
import { defineProps, toRefs, computed, reactive } from "vue";

const props = defineProps({
  sheepMax: Number,
});

// const { sheepMax } = toRefs(props);
// const sheepCount = ref(0);

// console.log(sheepCount.value)

// const checkBusy = computed(() => sheepCount.value >= sheepMax.value);

const { sheepMax } = toRefs(props);
const shepps = reactive([]);

const checkBusy = computed(() => shepps.length >= sheepMax.value);

const handleClick = () => {
  shepps.push(Math.floor(Math.random() * 6) + 1);
};
</script>

<style lang="scss" scoped>
#corral {
  display: flex;
  flex-wrap: wrap;
  min-height: 126px;
  margin: 10px;
  border: 3px solid;
  img {
    padding: 10px;
  }

  &::after {
    content: "";
    width: 0;
    height: 124px;
    flex-grow: 1;
    border-left: 2px solid;
    border-top: 2px solid;
  }
}
</style>
