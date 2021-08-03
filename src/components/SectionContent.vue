<template>
  <div :class="styleClass"><slot /></div>
</template>

<script setup>
import { defineProps, toRefs, computed } from "vue";

const props = defineProps({
  theme: String,
});
const { theme } = toRefs(props);

const CLASSES_AVALIBLES = {
  default: "",
  light: "light",
  dark: "dark",
};

const styleClass = computed(() => {
  const name = theme.value ?? "default";
  console.log(CLASSES_AVALIBLES.hasOwnProperty(name));
  return CLASSES_AVALIBLES.hasOwnProperty(name) ? CLASSES_AVALIBLES[name] : "";
});
</script>
<style lang="scss" scoped>
div {
  background-color: #bdbdbd;
  color: #000;
  font-size: 16px;
  margin: 10px;
  line-height: 16px;
  padding: 16px;
  .light {
    background-color: #fff;
    color: #212121;
    border: 1px solid #212121;
  }
  .dark {
    background-color: #121212;
    color: #fff;
  }
}
</style>
