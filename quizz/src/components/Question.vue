<script setup>
const props = defineProps({
  question: Object,
});
</script>

<template>
  <div class="question">
    <h3>{{ question.question }}</h3>
    <ul>
      <li v-for="(choice, index) in question.choices" :key="choice">
        <label :for="`answer${index}`">
          <input type="radio" name="answer" :id="`answer${index}`" />
          {{ choice }}
        </label>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.question {
  padding-top: 2rem;
}
</style>
