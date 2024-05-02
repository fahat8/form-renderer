<script setup lang="ts">
import { ref } from 'vue';
import Survey from './components/Survey.vue'
import SurveyCreator from './components/SurveyCreator.vue'

const isSurveyActive = ref(false);

</script>

<template>
  <div>
    <button @click="isSurveyActive = !isSurveyActive">
      {{ isSurveyActive ? 'Switch to Survey' : 'Switch to Survey Creator' }}
    </button>
    <SurveyCreator v-if="!isSurveyActive" />
    <Survey v-else />
  </div>
</template>

<style scoped>
button {
  margin-bottom: 20px;
  padding: 10px 20px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}
</style>