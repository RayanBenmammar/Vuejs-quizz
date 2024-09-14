<script setup>
import { computed, ref } from "vue";
import Progress from "./Progress.vue";
import Question from "./Question.vue";
const props = defineProps({
  quizz: Object,
});

const step = ref(0);
const question = computed(() => props.quizz.questions[step.value]);
const answers = ref(props.quizz.questions.map(() => null));

const addAnswer = (answer) => {
  answers.value[step.value] = answer;
  step.value++;
};
</script>

<template>
  <div>
    <h1>{{ quizz.title }}</h1>
    <Progress :value="step" :max="quizz.questions.length - 1" />
    <Question :question="question" @answer="addAnswer" v-if="question" />
  </div>
</template>
