<script setup>
import { shuffleArray } from "@/functions/array";
import { computed, onMounted, onUnmounted, ref } from "vue";
import Answer from "./Answer.vue";
const props = defineProps({
  question: Object,
});
const answer = ref(null);
const emits = defineEmits(["answer"]);
const hasAnswer = computed(() => answer.value !== null);
const randomQuestions = computed(() => shuffleArray(props.question.choices));
let timer;
const onAnswer = () => {
  clearTimeout(timer);
  timer = setTimeout(() => {
    emits("answer", answer.value);
  }, 1000);
};

onMounted(() => {
  timer = setTimeout(() => {
    answer.value = "";
    onAnswer();
  }, 5000);
});

onUnmounted(() => {
  clearTimeout(timer);
});
</script>

<template>
  <div class="question">
    <h3>{{ question.question }}</h3>
    <ul>
      <li v-for="(choice, index) in randomQuestions" :key="choice">
        <Answer
          :id="`answer${index}`"
          :disabled="hasAnswer"
          :value="choice"
          :correct_answer="question.correct_answer"
          v-model="answer"
          @change="onAnswer"
        />
      </li>
    </ul>
    <!-- <button :disabled="!hasAnswer" @click="emits('answer', answer)">
      Question suivante
    </button> -->
  </div>
</template>

<style scoped>
.question {
  padding-top: 2rem;
}

.question button {
  margin-left: auto;
  display: block;
}
</style>
