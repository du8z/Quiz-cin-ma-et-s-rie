<template>
  <section>
    <div>
      <h2>{{}}</h2>
    </div>
    <div></div>
    <div class="answers">
      <input type="radio" id="one" value="One" v-model="picked" />
      <label for="one">One</label>
      <input type="radio" id="one" value="Two" v-model="picked" />
      <label for="two">Two</label>
    </div>
  </section>
</template>

<style>
.answers > label > input {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 20px 10px;
}
</style>

<script setup>
import { ref, computed } from "vue";

// Déclaration des props
const props = defineProps({
  question: {
    type: Array,
    required: true,
  },
});
console.log(props);

// Variables réactives
const picked = ref("");

// Propriétés dérivées
// const questionText = computed(() => props.question.question);
// const choices = computed(() => props.question.choices);

console.log(questionText);
</script>
