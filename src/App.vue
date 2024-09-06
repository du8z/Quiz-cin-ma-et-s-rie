<template>
  <header>
    <h1 style="font-size: 20px; padding-bottom: 20px">
      Questionnaire sur les Films et Séries
    </h1>
  </header>
  <section style="margin: 20px 10vw">
    <!-- <ProgressBar /> -->
  </section>
  <section style="margin: 20px 10vw">
    <Fetch />
  </section>
</template>

<style>
* {
  margin: 0;
  padding: 0;
  font-family: "Courier New", Courier, monospace;
}

header {
  width: 100%;
  display: flex;
  align-items: start;
  justify-content: center;
  padding-top: 200px;
}
</style>

<script setup>
// import DataFetcher from "./components/DataFetcher.vue";
// import Question from "./components/Question.vue";
import ProgressBar from "./components/ProgressBar.vue";
import Fetch from "./components/Fetch.vue";

import { ref, watchEffect, toValue } from "vue";
</script>
