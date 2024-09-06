<template>
  <div>
    <ProgressBar
      :progressWidth="progressPercentage"
      style="margin-bottom: 50px"
    />
    <form
      v-if="items.questions && items.questions.length > 0"
      @submit.prevent="handleSubmit"
    >
      <div
        v-if="currentQuestionIndex < items.questions.length"
        style="display: flex; flex-direction: column; gap: 20px"
      >
        <h2>{{ items.questions[currentQuestionIndex].question }}</h2>
        <div
          v-for="(choice, index) in items.questions[currentQuestionIndex]
            .choices"
          :key="index"
        >
          <label>
            <input
              type="radio"
              :name="'question' + currentQuestionIndex"
              :value="choice"
              v-model="selectedAnswers[currentQuestionIndex]"
            />
            {{ choice }}
          </label>
        </div>
        <button
          @click="validateAnswer"
          style="
            margin-top: 20px;
            width: 200px;
            height: 40px;
            border-radius: 10px;
          "
        >
          Validez cette réponse
        </button>
      </div>

      <div v-else>
        <h2>Quiz terminé !</h2>
        <button type="submit">Voir les résultats</button>
        <ul>
          <li v-for="(i, index) in selectedAnswers">
            {{ items.questions[index].correct_answer }}
          </li>
        </ul>
      </div>
    </form>
  </div>
</template>

<script>
import ProgressBar from "./ProgressBar.vue";

export default {
  components: {
    ProgressBar,
  },
  data() {
    return {
      items: {}, // L'objet JSON qui contient les questions
      selectedAnswers: [], // Un tableau pour stocker les réponses sélectionnées
      currentQuestionIndex: 0, // L'index de la question courante
    };
  },
  computed: {
    // Calcule le pourcentage de progression
    progressPercentage() {
      // Vérifie que items.questions existe et qu'il a des questions
      if (this.items.questions && this.items.questions.length > 0) {
        return (this.currentQuestionIndex / this.items.questions.length) * 100;
      }
      return 0; // Si les questions ne sont pas encore chargées, retourne 0%
    },
  },
  mounted() {
    // Appel à une URL qui renvoie un fichier JSON
    fetch("../../data/quiz.json")
      .then((response) => response.json())
      .then((data) => {
        this.items = data;
        // Initialise le tableau des réponses sélectionnées avec des valeurs vides
        this.selectedAnswers = new Array(data.questions.length).fill("");
      })
      .catch((error) => {
        console.error("Erreur lors du chargement du JSON :", error);
      });
  },
  methods: {
    validateAnswer() {
      // Vérifie si une réponse a été sélectionnée avant de passer à la question suivante
      if (this.selectedAnswers[this.currentQuestionIndex] !== "") {
        this.currentQuestionIndex++;
      } else {
        alert("Veuillez sélectionner une réponse avant de valider.");
      }
    },
    handleSubmit() {
      console.log("Réponses sélectionnées :", this.selectedAnswers);
      // Ajoute ici la logique de traitement des réponses (validation, affichage des résultats, etc.)
    },
  },
};
</script>
