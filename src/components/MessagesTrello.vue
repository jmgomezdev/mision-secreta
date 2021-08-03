<template>
  <SectionContent
    v-for="(item, index) in messages"
    :key="index"
    :theme="item.theme"
  >
    <Cacatua
      v-if="item.secret === true && item.show === false"
      @click="handleClick(index)"
    />
    <div v-else>
      {{ item.message }}
    </div>
  </SectionContent>
</template>



<script setup>
import SectionContent from "./SectionContent.vue";
import Cacatua from "./Cacatua.vue";
import { reactive } from "@vue/reactivity";
// import { ref, computed, onMounted } from "vue";
async function getData(url) {
  try {
    const res = await fetch(url);
    const data = await res.json();
    return data;
  } catch {
    alert("No se ha podido obtener los datos");
    return null;
  }
}
// const messages = ref(null);
// onMounted(async () => {
//   console.log("Component mounted!");
//   messages.value = await fetch(
//     `https://trello.com/b/IUOxOY5z/misi%C3%B3n-secreta-cms.json`
//   ).then((a) => a.json());
//   console.log(messages.value);
// });

const data = await getData(
  `https://trello.com/b/IUOxOY5z/misi%C3%B3n-secreta-cms.json`
);
const messages = reactive(
  data?.cards.reduce(
    (acc, el) =>
      acc.concat({
        message: el?.desc,
        theme: el?.labels.some((label) => label.name === "theme-dark")
          ? "dark"
          : "light",
        secret: el?.name.includes("secreto"),
        show: false,
      }),
    []
  )
);

function handleClick(key) {
  console.log(key);
  messages[key]["show"] = true;
}
</script>
