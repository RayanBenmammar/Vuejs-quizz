<script setup>
import { computed } from "vue";

const props = defineProps({
  quizz: Object,
  answers: Array,
});

const score = computed(() => {
  return props.quizz.questions.reduce((acc, question, i) => {
    if (question.correct_answer === props.answers[i]) {
      return acc + 1;
    }
    return acc;
  }, 0);
});

const hasWon = computed(() => score.value >= props.quizz.minimum_score);
</script>

<template>
  <h1>Recapitulatif</h1>
  <p>{{ hasWon ? quizz.success_message : quizz.failure_message }}</p>
  <p>Score : {{ score }} / {{ props.quizz.questions.length }}</p>
</template>
