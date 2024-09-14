<script setup>
import { ref } from "vue";
import Progress from "./Progress.vue";
defineProps({
  quizz: Object,
});

const step = ref(0);
</script>

<template>
  <div>
    <h1>{{ quizz.title }}</h1>
    <Progress :value="step" :max="quizz.questions.length - 1"></Progress>
  </div>
</template>
