<template>
    <div>
      <h4 class="mb-4">Filière et parcours</h4>
  
      <!-- Sélection de la filière -->
      <div class="mb-4">
        <label class="form-label">Filière</label>
        <div v-for="major in Object.keys(majorsTracks)" :key="major" class="form-check mb-2">
          <input 
            class="form-check-input" 
            type="radio" 
            :id="major"
            :value="major"
            v-model="formData.major"
          >
          <label class="form-check-label" :for="major">
            {{ major }}
          </label>
        </div>
      </div>
  
      <!-- Sélection du parcours (s'affiche seulement si une filière est choisie) -->
      <div class="mb-3" v-if="availableTracks.length > 0">
        <label class="form-label">Parcours</label>
        <select 
          class="form-select" 
          v-model="formData.track"
          :class="{ 'is-invalid': validationErrors.track }"
        >
          <option value="">Sélectionnez un parcours</option>
          <option v-for="track in availableTracks" :key="track" :value="track">
            {{ track }}
          </option>
        </select>
      </div>
    </div>
  </template>
  
  <script setup lang="ts">
  import { computed } from 'vue'
  
  const props = defineProps<{
    formData: {
      major: string
      track: string
    }
    validationErrors: {
      track: boolean
    }
  }>()
  
  // Liste des filières et de leurs parcours
  const majorsTracks = {
    'Informatique': ['BDGL', 'Réseau et Système'],
    'Droit': ['Droit Privé (DPR)', 'Droit Public (DPU)'],
    'Économie': ['Développement Agricole Durable', 'Économie et Politique de l\'Environnement'],
    'Gestion': ['Finance', 'Comptabilité et Audit', 'Management et Organisation'],
    'Commerce': ['Commerce'],
    'Communication et Information': ['Communication des Organisations', 'Communication et Information des Entreprises', 'Média', 'Journalisme'],
    'Génie Industrielle': ['Génie Industrielle et Maintenance', 'Génie Électronique et Informatique Industrielle', 'Production et Maintenance'],
    'Télécommunication': ['Génie des Réseaux et Transformation', 'Génie des Radiocommunications']
  }
  
  // Filtrer les parcours disponibles selon la filière sélectionnée
  const availableTracks = computed(() => {
    return props.formData.major ? majorsTracks[props.formData.major] || [] : []
  })
  </script>
  