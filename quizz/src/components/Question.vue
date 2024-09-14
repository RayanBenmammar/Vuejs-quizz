<script setup>
import { computed, ref } from "vue";
const props = defineProps({
  question: Object,
});
const answer = ref(null);
const emits = defineEmits(["answer"]);
const hasAnswer = computed(() => !!answer.value);
</script>

<template>
  <div class="question">
    <h3>{{ question.question }}</h3>
    <ul>
      <li v-for="(choice, index) in question.choices" :key="choice">
        <label :for="`answer${index}`">
          <input
            type="radio"
            name="answer"
            :id="`answer${index}`"
            :value="choice"
            v-model="answer"
          />
          {{ choice }}
        </label>
      </li>
    </ul>
    <button :disabled="!hasAnswer" @click="emits('answer', answer)">
      Question suivante
    </button>
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
