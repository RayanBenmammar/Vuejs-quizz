<script setup>
import { onMounted, ref } from "vue";
import Quizz from "./components/quizz.vue";

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
  <div class="container">
    <div v-if="state === 'error'">
      <p>Impossible de charger le questionnaire</p>
    </div>
    <div :aria-busy="state === 'loading'">
      <Quizz :quizz="quizz" v-if="quizz"></Quizz>
    </div>
  </div>
</template>

<style scoped>
.container {
  margin-top: 2rem;
}
</style>
