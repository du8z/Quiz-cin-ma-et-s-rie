<template>
  <div class="globalContaier">
    <div class="progress-bar-container">
      <div class="progress-bar" :style="{ width: progressWidth + '%' }"></div>
    </div>
    <!-- <button @click="increaseProgress">Augmenter</button> -->
    <!-- <button @click="decreaseProgress">Diminuer</button> -->
    <p>{{ progressWidth }} %</p>
  </div>
</template>

<style>
.progress-bar-container {
  width: 100%;
  height: 30px;
  background-color: #e0e0e0;
  border-radius: 5px;
  overflow: hidden;
}

.progress-bar {
  height: 100%;
  background-color: #76c7c0;
  width: 0%;
  transition: width 0.3s ease;
}
.globalContaier {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 0 50px;
}
p {
  padding-left: 20px;
  min-width: 70px;
}
</style>

<script setup>
import { ref, defineProps } from "vue";
const props = defineProps({
  progressWidth: {
    type: Number,
    required: true,
  },
});

// const progressWidth = ref(50);

const increaseProgress = () => {
  progressWidth.value += 20;
};

const decreaseProgress = () => {
  progressWidth.value -= 20;
};
</script>
