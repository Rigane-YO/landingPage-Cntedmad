<template>
    <div>
      <h4 class="mb-4">Niveau d'étude</h4>
      <div class="mb-3">
        <div v-for="level in studyLevels" :key="level" class="form-check mb-2">
          <input 
            class="form-check-input" 
            type="radio" 
            :id="level"
            :value="level"
            v-model="formData.studyLevel"
          >
          <label class="form-check-label" :for="level">
            {{ level }}
          </label>
        </div>
      </div>
    </div>
  </template>
  
  <script setup lang="ts">
  defineProps<{
    formData: {
      studyLevel: string
    }
  }>()
  
  const studyLevels = ['L1', 'L2', 'L3', 'M1', 'M2']
  </script>
  