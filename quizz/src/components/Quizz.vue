<script setup>
import { computed, ref } from "vue";
import Progress from "./Progress.vue";
import Question from "./Question.vue";
import Recap from "./Recap.vue";
const props = defineProps({
  quizz: Object,
});

const state = ref("question");
const step = ref(0);
const question = computed(() => props.quizz.questions[step.value]);
const answers = ref(props.quizz.questions.map(() => null));

const addAnswer = (answer) => {
  answers.value[step.value] = answer;
  if (step.value === props.quizz.questions.length - 1) {
    state.value = "recap";
  } else {
    step.value++;
  }
};
</script>

<template>
  <div>
    <h1>{{ quizz.title }}</h1>
    <Progress :value="step" :max="quizz.questions.length - 1" />
    <Question
      :key="question.question"
      :question="question"
      @answer="addAnswer"
      v-if="state === 'question'"
    />
    <Recap :quizz="props.quizz" :answers="answers" v-if="state === 'recap'" />
  </div>
</template>
