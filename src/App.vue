<script setup lang="ts">
import { ref } from 'vue';
import Survey from './components/Survey.vue'
import SurveyCreator from './components/SurveyCreator.vue'
import SurveyCreator2 from './components/SurveyJsonGenerator.vue';

const activeComponent = ref('Survey'); // Default component to show

function toggleComponent() {
  if (activeComponent.value === 'Survey') {
    activeComponent.value = 'SurveyCreator';
  } else if (activeComponent.value === 'SurveyCreator') {
    activeComponent.value = 'SurveyCreator2';
  } else {
    activeComponent.value = 'Survey';
  }
}

</script>

<template>
  <div>
    <button @click="toggleComponent">
      Switch View
    </button>
    <SurveyCreator v-if="activeComponent === 'SurveyCreator'" />
    <SurveyCreator2 v-if="activeComponent === 'SurveyCreator2'" />
    <Survey v-if="activeComponent === 'Survey'" />
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