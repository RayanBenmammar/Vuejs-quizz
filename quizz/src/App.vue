<script setup>
import { onMounted, ref } from "vue";

const quizz = ref(null);
const state = ref("loading");

onMounted(() => {
  fetch("/quizz.json")
    .then((response) => {
      if (response.ok) {
        return response.json();
      } else {
        throw new Error("Failed to fetch quiz data");
      }
    })
    .then((data) => {
      quizz.value = data;
      state.value = "loaded";
    })
    .catch((error) => {
      state.value = "error";
    });
});
</script>

<template>
  <div v-if="state === 'error'">
    <p>Impossible de charger le questionnaire</p>
  </div>
  <div :aria-busy="state === 'loading'">{{ quizz }}</div>
</template>

<style scoped></style>
