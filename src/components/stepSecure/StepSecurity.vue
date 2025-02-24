<template>
    <div>
      <h4 class="mb-4">Sécurité</h4>
      <div class="mb-3">
        <label class="form-label">Mot de passe</label>
        <input 
          type="password" 
          class="form-control" 
          v-model="formData.password"
          :class="{ 'is-invalid': validationErrors.password }"
        >
      </div>
      <div class="mb-3">
        <label class="form-label">Confirmer le mot de passe</label>
        <input 
          type="password" 
          class="form-control" 
          v-model="formData.confirmPassword"
          :class="{ 'is-invalid': passwordMismatch }"
        >
      </div>
      <div v-if="passwordMismatch" class="alert alert-danger">
        Les mots de passe ne correspondent pas
      </div>
    </div>
  </template>
  
  <script setup lang="ts">
  import { computed } from 'vue'
  
  const props = defineProps<{
    formData: {
      password: string
      confirmPassword: string
    }
    validationErrors: {
      password: boolean
    }
  }>()
  
  const passwordMismatch = computed(() => {
    return props.formData.password !== props.formData.confirmPassword
  })
  </script>
  