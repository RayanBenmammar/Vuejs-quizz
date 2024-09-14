<script setup>
import { computed } from "vue";

const props = defineProps({
  id: String,
  disabled: Boolean,
  value: String,
  correct_answer: String,
});

const model = defineModel();
const classes = computed(() => ({
  disabled: props.disabled,
  right: props.disabled && props.value === props.correct_answer,
  wrong:
    props.disabled &&
    props.value !== props.correct_answer &&
    model.value === props.value,
}));
</script>

<template>
  <label :for="id" :class="classes">
    <input
      type="radio"
      name="answer"
      :id="id"
      :value="value"
      :disabled="disabled"
      v-model="model"
    />
    {{ value }}
  </label>
</template>

<style scoped>
.right {
  color: green;
}

.wrong {
  color: red;
}

.disabled {
  opacity: 0.5;
}
</style>
