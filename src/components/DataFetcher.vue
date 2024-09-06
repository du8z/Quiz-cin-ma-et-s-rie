<template>
  <div>
    <Question v-if="data.questions" :questions="data.questions" />
    <h1>{{ data.title }}</h1>
    <p v-if="error">{{ error }}</p>
    <ul v-if="data.questions">
      <h2>{{ question }}</h2>
      <li v-for="(question, index) in data.questions" :key="index">
        {{ question.choices[1] }}
      </li>
    </ul>
  </div>
</template>

<script>
import Question from "./Question.vue";
import { ref } from "vue";

export default {
  components: {
    Question,
  },
  data() {
    return {
      data: {},
      error: null,
    };
  },
  mounted() {
    this.fetchData();
  },
  methods: {
    async fetchData() {
      try {
        const response = await fetch("../../data/quiz.json");
        if (!response.ok) {
          throw new Error("Erreur lors du chargement des données");
        }
        this.data = await response.json();
        console.log(this.data);
      } catch (error) {
        this.error = error.message;
      }
    },
  },
};
</script>
