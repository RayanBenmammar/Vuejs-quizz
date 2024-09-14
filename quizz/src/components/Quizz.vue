<script setup>
import { computed, ref } from "vue";
import Progress from "./Progress.vue";
import Question from "./Question.vue";
const props = defineProps({
  quizz: Object,
});

const step = ref(0);
const question = computed(() => props.quizz.questions[step.value]);
</script>

<template>
  <div>
    <h1>{{ quizz.title }}</h1>
    <Progress :value="step" :max="quizz.questions.length - 1" />
    <Question :question="question" v-if="question" />
  </div>
</template>
