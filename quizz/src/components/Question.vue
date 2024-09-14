<script setup>
const props = defineProps({
  question: Object,
});
</script>

<template>
  <div class="question">
    <h3>{{ question.question }}</h3>
  </div>
</template>

<style scoped>
.question {
  padding-top: 2rem;
}
</style>
